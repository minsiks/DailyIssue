# 23-10-16 Program List- Day 04

```
문제 사항
1----------------------
기본사업 > 사업관리> 사업계획>세부사업계획서관리>다문화>리스트에서 보류/결쟈
- mcultProgramService.withrawListMcultProgra
- mcultProgramService.approvalList
상응하는 sql문 없음

>> 오류 검출 안됨

2-------------------------
기본사업> 사업관리 > 사업실적관리 > 패밀리넷 등록/수정
- SEQ_TFAMILYNET_PROGRAM.NEXTVAL 시퀀스 DB에 존재하지 않음
- 그전에는 되었었던듯
>>>> 해결

5------------
기본사업> 사업관리 > 사업운영 > 반(모임)/프로그램 관리
- 가족, 홍보,방문 프로그램 셀렉 옵션 안뜸
- 기존 페이지와 동일한 param과 동일한 경로로 데이터를 보내도 쿼리에서 안뽑아짐
- ex)/* McultProgram_SQL.xml McultProgram14DAO.selectMcultProgramListCommon_doublelang */

>>>>>>>>>>>>> 년도를 바꾸니 정상 작동 (데이터 부재)

6-------------
별도사업 > 가족희망드림지원사업 > (취약위기)사례관리 > 초기상담
신규 성명 /restApi/selectCaseFamilyMember.do 동작안됨 

>>>>>> 서버 올라간것 해결 확인


```

```
원래도 안되는항목
- 상담관리(일반)>건강가정>내담자 등록 후 수정 
- 실적관리 > 사업실적관리 > 가족서비스/기본 
	*종료된 프로그램 출석 클릭시 error 페이지
```

```메모
기본사업 THEALTHPROGRAMBASISRESULT_A 테이블 BASIS_ACHIEVEMENT_NO == 
패밀리넷 TFAMILYNET_PROGRAM_DETAIL 테이블 PG_DETAIL_NO
기본사업 BIZ_NO == 패밀리넷 FAMILYNET_PG_NO

PG_DETAIL_NO, MEMBER_ID, ATTENDYX, (SYS_GUBUN) 최소 필요한 테이블 컬럼 건강가정도 동일
```

```

```

