# 23-12-13 Program List- Day 05

### 공통 Search Area 통합 

- 초기 시작 방법 

  - 통합전에도 센터 셀렉트 value가 같은 text라도 다르게 (가족서비스-다문화,한국어-건가) 나온다고 알고 있어서 common.js에 각 

    - /CommonCode/CenterDropDown.do 가족서비스

      - ```sql
        SELECT FACILITY_NO AS MULTIVALUE,
           FACILITY_NAME AS MULTIOPTION
        FROM TFACILITY_A 
        WHERE 1=1
        AND USE_YN = 'Y' AND DEL_YN = 'N'
        AND FACILITY_SECT != 'FCLTT00009' /* 한국어교육 관련코드 제외*/          
        AND FACILITY_NO <> '00000' 
        AND FACILITY_NO <> '00001' 
        AND FACILITY_NO <> '99999' 
        AND SERVICE_ADMIN_ZONE_CODE   LIKE SUBSTR('2600000000',0,2)||'%'
        ORDER BY FACILITY_NAME
        
        ```

    - /CommonCode/CenterDropDownMcult.do

      - ```sql
        SELECT FACILITY_NO AS MULTIVALUE,
           FACILITY_NAME AS MULTIOPTION
        FROM TFACILITY 
        WHERE 1=1
        AND USE_YN = 'Y' AND DEL_YN = 'N'
        AND FACILITY_SECT != 'FCLTT00009' /* 한국어교육 관련코드 제외*/
        AND FACILITY_NO <> '00000' 
        AND FACILITY_NO <> '00001' 
        AND FACILITY_NO <> '99999' 
        AND DUTY_REALM_SECT = 'FCDTA00002' 
        AND SERVICE_ADMIN_ZONE_CODE   LIKE SUBSTR('2600000000',0,2)||'%'
        ORDER BY FACILITY_NAME
        
        ```

    - /CommonCode/CenterDropDownHealth.do 건강가정

      - ```sql
        SELECT FACILITY_NO AS MULTIVALUE,
           FACILITY_NAME AS MULTIOPTION
        FROM TFACILITY 
        WHERE 1=1
        AND USE_YN = 'Y' AND DEL_YN = 'N'
        AND FACILITY_SECT != 'FCLTT00009' /* 한국어교육 관련코드 제외*/
        AND FACILITY_NO <> '00000' 
        AND FACILITY_NO <> '00001' 
        AND FACILITY_NO <> '99999' 
        AND DUTY_REALM_SECT = 'FCDTA00001' 
        AND SERVICE_ADMIN_ZONE_CODE   LIKE SUBSTR('2600000000',0,2)||'%'
        ORDER BY FACILITY_NAME
        
        ```

    - /CommonCode/CenterDropDown_K.do 한국어

      - ```sql
        SELECT FACILITY_NO AS MULTIVALUE,
           FACILITY_NAME AS MULTIOPTION
        FROM TFACILITY 
        WHERE 1=1
        AND USE_YN = 'Y' AND DEL_YN = 'N'
        AND FACILITY_NO <> '00000' 
        AND FACILITY_NO <> '00001' 
        AND FACILITY_NO <> '99999' 
        AND DUTY_REALM_SECT = 'FCDTA00002' 
        AND SERVICE_ADMIN_ZONE_CODE   LIKE SUBSTR('2600000000',0,2)||'%'
        ORDER BY FACILITY_NAME
        ```

  - 으로 4가지의 버전으로 현재운영에서 Controller 한 메소드안에서 session 변경적용되어 세션값을 추출하여 분기하는 방법을 피하고 아예 컨트롤러의 다른메소드를 향하도록 변경

  - 기존은 changesession했을시 직무구분을 변경시키며 다른 조건값을 변경

    - 현재는 화면마다 파람으로 아예 다른 컨트롤러로 가도록 변경

  - 하지만 기존 session change를 할경우 ${loginVo.FACILITY_NO}와 ${loginVO.facility_sect},'${loginVO.duty_realm_sect}'가 변경 적용되는 부분은 login 할때 아래의 쿼리에서 , *로그인 할 시, 해당 아이디의 직무와 권환을 조회하여 리스트로 뽑음 ` LEFT JOIN TFACILITY facility ON facility.FACILITY_NO  = employeecontract.FACILITY_NO` fcility를 join하여 ,facility.DUTY_REALM_SECT DUTY_REALM_SECT (직무 분야 구분)을 조회

```sql
SELECT
                employee.EMPLOYEE_NO
                ,employeecontract.FACILITY_NO                       /** 계약에 센터코드*/
                ,UFN_GET_FACILITYNAME(employeecontract.FACILITY_NO )     FACILITY_NAME
                ,facility.DUTY_REALM_SECT DUTY_REALM_SECT   <- 추가 된 소스
                ,employeecontract.ADMIN_ZONE_CODE                    /** 계약에 지역코드*/
                ,UFN_GET_LEGALDONGNAME(employeecontract.ADMIN_ZONE_CODE)   ADMIN_ZONE_CODE_NAME
                ,employee.NAME EMPLOYEE_NAME
                ,employeecontract.CONTRACT_SECT                         /** 계약구분 */
                ,employeecontract.WORK_BEGIN_DATE                       /** 계약 시작일*/
                ,employeecontract.WORK_END_DATE                         /** 계약 종료일*/
                ,employeecontract.CONTRACT_NO                            /** 계약 번호*/   
                ,employeeduty.DUTY_SECT                                   /** 직무 구분*/
                ,UFN_GET_CODENAME(employeeduty.DUTY_SECT ) DUTY_SECT_NAME
                ,employeeduty.EMPLOYEE_DUTY_NO                            /** 직무 번호*/
                ,employeeduty.DUTY_BEGIN_DATE                       /** 직무 시작일*/
                ,employeeduty.DUTY_END_DATE                         /** 직무 종료일*/
                ,coach.COACH_NO                                        /** 지도사번호*/
                ,coach.COACH_SECT                                      /** 지도사 구분*/
                ,UFN_GET_CODENAME(coach.COACH_SECT) COACH_SECT_NAME
                ,coach.CARDINAL_NO                                      /**기수*/
                ,UFN_GET_CODENAME(coach.INTERPRET_HUMANFORCE_SECT)  HUMANFORCE_SECT_NAME /**등급명*/
                ,employee.sido_public_servant_region
            FROM TEMPLOYEE    employee     /** 직원 테이블*/
            INNER JOIN  TEMPLOYEECONTRACT employeecontract /** 계약 테이블*/
	            ON employeecontract.EMPLOYEE_NO = employee.EMPLOYEE_NO     
	            AND  employeecontract.USE_YN = 'Y' AND employeecontract.DEL_YN = 'N'
	            AND employeecontract.WORK_BEGIN_DATE <= TO_CHAR(SYSDATE, 'YYYYMMDD')
	            AND employeecontract.WORK_END_DATE >= TO_CHAR(ADD_MONTHS(SYSDATE,-2), 'YYYYMMDD')
            INNER JOIN TEMPLOYEEDUTY employeeduty ON  employeeduty.CONTRACT_NO = employeecontract.CONTRACT_NO /** 직무 테이블*/
	            AND  employeeduty.USE_YN = 'Y' AND employeeduty.DEL_YN = 'N' 
            LEFT JOIN TCOACH  coach ON coach.CONTRACT_NO = employeeduty.CONTRACT_NO  /** 지도사 테이블*/
            AND  coach.USE_YN = 'Y' AND coach.DEL_YN = 'N'      
            LEFT JOIN TFACILITY facility ON facility.FACILITY_NO  = employeecontract.FACILITY_NO
            WHERE 1=1
            AND  employee.EMPLOYEE_NO = '00000000000000014043'
			AND  employee.USE_YN = 'Y' AND employee.DEL_YN = 'N';
```

- 직무 구분을 조회하여 각 다문화, 건강가정의 FACILITY_NO을 리스트로 조회

  - 파악한 바로는 건강가정의 facility_no와 facility_sect는 loginVo.facility_no_a와 loginVo.facility_sect_a로 별개로 세팅되어있어서 문제가 많이 되지 않음
  - 문제 다문화, 건강가정이 no가 다름
    - 다문화와, 한국어는 조회되는 쿼리는 다르지만 동일한 DUTY_REALM_SECT를 기준으로 조회
    - 그렇게에 다문화, 한국어 value, 즉  facility_no가 동일

- CmmSymMnuController의 기존코드 활용하여 로그인 해서 메인화면 진입할때 각 loginVo의 mult_facility_no와 health_facility_no를 삽입

  - ```java
    /**
    	 * 메인페이지
    	 * @param request
    	 * @param model
    	 * @param session
    	 * @return
    	 * @throws Exception
    	 */
    	@RequestMapping("/cmm/main/AcvMngMainPage.do")
    	public String setContent(HttpServletRequest request, ModelMap model, HttpSession session) throws Exception{
    
    		//sso 관련하여 코드 추가
        	String login_id = request.getParameter("login_id");
        	String token_id = request.getParameter("token_id");
        	
        	LOGGER.debug("URL :: /cmm/main/AcvMngMainPage.do || login_id : {}", login_id);
        	LOGGER.debug("URL :: /cmm/main/AcvMngMainPage.do || token_id: {}", token_id);
        	
    		LoginVO login = (LoginVO)EgovUserDetailsHelper.getAuthenticatedUser();
    				
        	if( null != login_id && null != token_id ){
        		login.bFromOthersite = true;
        		login.setbFromOthersite(true);
        	}
    		
        	//저장된 로그인 정보 확인
    		for (java.lang.reflect.Field field : login.getClass().getDeclaredFields()){
    			field.setAccessible(true);
    			Object value=field.get(login);
    			if (value != null)
    				System.out.println(field.getName()+","+value);
    		}
    		
        	login.setLogin_ip(EgovClntInfo.getClntIP((HttpServletRequest) request));
        	login.setCurrent_login_ip(EgovClntInfo.getClntIP((HttpServletRequest) request));
    		
        	//기본권한 이외에 시도공무원,여가부공무원 권한만 가지고 있으면 메인을 보여주지 않는다.
    		String nomain = "N";
    		
    	   	InetAddress inet = InetAddress.getLocalHost();
        	request.getSession().setAttribute("clientip", request.getRemoteAddr());
        	request.getSession().setAttribute("clienthost", request.getRemoteHost());
        	request.getSession().setAttribute("servername", inet.getHostName());
        	request.getSession().setAttribute("serverip", inet.getHostAddress());
        	
        	login.setLogin_ip(request.getRemoteAddr());
    
    	    	// 시스템 별로 처음 화면 분기
    	    //***************************//
    	    
    		LogInInfoVO logInInfoVO = new LogInInfoVO();
    		logInInfoVO.setEmployee_no(login.getEmployee_no());
    		
    		// 계약정보가 없습니다.
    		List<EmployeeDutyVO> duty_list = kihfisLoginDAO.selectEmployeeDutyList(logInInfoVO);
    		if(duty_list != null && duty_list.size() == 0){
    			login.setFamily_yn("N");
    			}else {
    				for(int i = 0, n = duty_list.size() ; i < n ; i++){
    					EmployeeDutyVO employeeDutyVO = duty_list.get(i);
    					if(employeeDutyVO.getDuty_realm_sect().equals("FCDTA00002")) { // 다문화
    						login.setMcult_facility_no(employeeDutyVO.getFacility_no());
    					}
    					if(employeeDutyVO.getDuty_realm_sect().equals("FCDTA00001")) { // 건가
    						login.setHealth_facility_no(employeeDutyVO.getFacility_no());
    					}
    			}
    		} 
    		
    		sessionUtil.setSessionLoginEntitiy(null);
       	
    		// 실적 관리 시스템
        	if("Y".equals(login.getAcvm_yn())) { 		
    			List<String> authorList = EgovUserDetailsHelper.getAuthorities();
    			login.setSystem_sel("1");
    			
    	    	for(String author : authorList){
    	    		if("ROLE_ANONYMOUS".equals(author) || "ROLE_USER".equals(author)){	//기본권한
    	    			continue;
    	    		}
    	    		if(author.equals("ROLE_SIDO_PUBSVT") || author.equals("ROLE_MOGEF_PUBSVT")){	//시도공무원 //여가부공무원
    	    			nomain="Y";
    				}else{
    					nomain="N";
    					break;
    				}
    	    	}
    	    	
    		} else if("Y".equals(login.getFamily_yn())) { 		// 가족지원 통합 시스템 
    			
    			branchUtil.actionloginNoSSO_T(login, model, request, session, "0");
    			login.setSystem_sel("0");
    			request.getSession().setAttribute("System_sel", "0");
            	
    		} else if("Y".equals(login.getLecture_yn()) || "Y".equals(login.getKorea_yn())) { 
    			branchUtil.actionloginNoSSO_T(login, model, request, session, "0");
    			
    			login.setSystem_sel("2");
    			request.getSession().setAttribute("System_sel", "2");
    		} else if("Y".equals(login.getEbusiness_yn())) { 
    			request.getSession().setAttribute("System_sel", "3");
    		}
        	//메뉴정보 가져오기
        	acvMngLeftMenufirst(new CmmSymMnuVO(), "", "", "", "", session, model, request);
        	
        	// 연도 정보를  저장
        	Calendar calendar = Calendar.getInstance();
        	int year = calendar.get(Calendar.YEAR);
        	request.getSession().setAttribute("currentYear", year);
    
        	List<TestSelectVo> yearList = new ArrayList<TestSelectVo>();
        	TestSelectVo testSelectVo = new TestSelectVo();
        	for(int i = (year-6), n = (year) ; i <= n ; i++){
        		testSelectVo = new TestSelectVo();
        		testSelectVo.setCode_name(i+"");
        		testSelectVo.setCode_type(i+"");
        		testSelectVo.setCode_value(i+"");
        		yearList.add(testSelectVo);
        	}
    
        	request.getSession().setAttribute("loginVO", login);
        	request.getSession().setAttribute("loginSessionId", login.getLogin_id());
        	request.getSession().setAttribute("orgLoginVO", login);
        	request.getSession().setAttribute("userName", login.getName());
        	request.getSession().setAttribute("facilityName", login.getFacility_name());
            request.getSession().setAttribute("areaName", login.getAdmin_zone_code_name());
            request.getSession().setAttribute("intr_budget_sect", login.getIntr_budget_sect());
            request.getSession().setAttribute("password_change_dt", login.getPassword_change_dt());
            request.getSession().setAttribute("employee_no", login.getEmployee_no());
            request.getSession().setAttribute("yearList", yearList); //2022-07-19 연도 추가
    		
        	model.addAttribute("loginVO", login);
        	model.addAttribute("loginSessionId", login.getLogin_id());
        	model.addAttribute("orgLoginVO", login);
        	model.addAttribute("userName", login.getName());
        	model.addAttribute("facilityName", login.getFacility_name());
        	model.addAttribute("areaName", login.getAdmin_zone_code_name());
        	model.addAttribute("intr_budget_sect", login.getIntr_budget_sect());
        	model.addAttribute("password_change_dt", login.getPassword_change_dt());
        	model.addAttribute("employee_no", login.getEmployee_no());    	
        	
        	
        	model.addAttribute("yearList", "yearList");
        	model.addAttribute("nomain", nomain);	
        	model.addAttribute("loginVO", login);
        	
        	return "com/main/AcvMngMainView";
    	}
    ```

  - '${loginVO.mcult_facility_no}','${loginVO.health_facility_no}' 로 적용 

``` 
추가이슈 : 쓰고있는 jsp도 가족서비스면 acvmng/common.js - 건강가정 khifis/common.js - 한국어면 kihfiske/common.js
```



```apah
<c:if test="${fn:indexOf(chk, 'mcult') > -1 || fn:indexOf(chk, 'health') > -1 || fn:indexOf(chk, 'health') > -1}">

</c:if>
<c:if test="${fn:indexOf(chk, 'acvmng') > -1}">

</c:if>
```

