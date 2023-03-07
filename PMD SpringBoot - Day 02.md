# 23-3-7 PMD SpringBoot Day 02

### pmd사용 정적 코드 분석

- VariableNamingConventions
  - 스네이크케이스 -> 카멜케이스 변경
  - MyBaits와 충돌
  - 카멜케이스 적용 후에도 파라미터 변수명 오류


> SettlementInfo.java 똑같은 변수명 (camel,snake 케이스 둘다 존재) 
>
> - 카멜케이스로 변환중이기때문에 prodOrderSeq를 prodOrderSeqList로 변경 
