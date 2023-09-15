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
