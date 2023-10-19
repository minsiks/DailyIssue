# 23-10-16 Program List- Day 04

## BB_BM_CA_021_1

- 상담관리 (건강가정)
  - 상단 다문화 건강가정 라디어버튼 크기 다름
    - 원인 : IBSHEET들어오면 크기 바뀜

- 사업실적관리
  - 프로그램 등록 - 패밀리넷 
    - 주소찾기 파일찾기 등등 공통 아직 안함
  - 기본 등록
    - "/single/bm/sm/healthProgramBasisList_A.do"이게 뭔
    - 신청자가 없어서 등록을 할 수 없
  - 타일즈 ajaxResult 사용 못

```완료리스트
완료리스트
- 연간사업계획서관리
- 
```

### 연간사업계획서관리

- 다문화 신규 등록 DECIDE_REQUEST_NO 퍼링키 문제

  - ![2023-10-18 16 32 18](C:\Users\min\Documents\DailyIssue\assets\2023-10-18 16 32 18.png)

  - 새로 인서트문인데 DECIDE_REQUEST_NO를 참조하고 있어 무결성 오류
  - kihfis.com.cmm.service.impl.CommonServiceImpl 참고

- 건강가정 common list 약간 위에 여백 어떻게?

