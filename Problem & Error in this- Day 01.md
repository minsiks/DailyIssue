# 23-9-5 Problem & Error in this

## 문제 사항

### sun.misc.BASE64Encoder 임포트가 안됨

- Complier > Error/Warnings로 이동해서 
- Deprecated and restricted API
- Forbidden reference (access rules) 의 값을 Error -> Warning
- project > clean 
- Problems view 항목에서 에러를 선택해서 삭제하고 컴파일

> 또는 **설치된 JDK경로로 변경해준다**

#### 위의 방법으로는 실질적인 해결이 되지 않아 JDK 1.8을 다운로드받아서 해당 프로젝트에 넣어주었더니 해결!











### edge에서 dup없이 central에서 dup 발생 케이스 

- 파일명 다르지만 주요 정보(lotNo,Conr_No,Line_Num..)들이 동일한 이미지 파일이 동시에 전송받을 시 
  - ex) 파일명 중 serialNum만 다를 경우
    - Xray_G6037D7CP7610089_20430628000005_Stack02 VISION1_TEST1.bmp
    - Xray_G6037D7CP7610089_20430628000005_Stack02 VISION1_TEST.bmp

