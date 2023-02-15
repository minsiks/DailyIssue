# 23-2-15 Change SpringBoot From Spring- Day 07

### Admin 상점관리 spring->springboot 고도화

#### 1. 상품관리 디테일페이지 

- img 또는 설명upload가 잘 되어있지만 Failed to load plugin url: http://127.0.0.1:18181/js/tinymce/langs/.js 오류 발생
  - language 설정 오류로 수정후 해결
- bullet mandatory 아이콘 X
  - 해결 : th:text를 한 태그 안에는 th:text한 값들을 제외한 어떠한 글, 태그들은 사라진다. 태그안에 무언가 있다면, [[${}]]를 권장

#### 2. 코드관리

- CodeController.java parent가 null이여서 thymeleaf 에러 (parent의 존재의의?)

```java
	@RequestMapping(value = "insert", method = RequestMethod.POST)
	public String insert(Model model, Code parent,HttpServletRequest request) {
		model.addAttribute("languageCodeList", codeService.getLanguageList());
		model.addAttribute("parent", codeService.getCode(parent)); //null
		return thisUrl + "/insert";
	}
```

- 해결 : 단순 타임리프 문법 오류

#### 3. 사용자 그룹 관리

- popup창에서 swal 안뜸
  - controller 작성 오류 해결



> 해결못한 문제 : 
>
> 1. 엑셀 다운로드 : JSP에서도 기능 X  
>
> 2. 팝업 타임리프에서는 잘뜨는데 jsp에서는 안뜨는 현상
>
> 3. 딜리버리 트래킹 종료된 키 값
>
>    DeliveryCode.java에서
>
>    private String t_key = "ZBDehDj92gWtK79HITajgA";
>
>    ```xml
>    <Result>
>    <status>false</status>
>    <message>키 정보를 찾을수 없습니다. 종료된 키 or 유효하지 않은 키입니다.</message>
>    <Code>101</Code>
>    </Result>
>    ```
>
> 4. paging count 18일때 1/1 26일때 1/2 
>
> 5. admin-common-file, admin-popup의 정체
