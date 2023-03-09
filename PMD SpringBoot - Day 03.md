# 23-3-8 PMD SpringBoot Day 03

### pmd사용 정적 코드 분석

- VariableNamingConventions
  - 스네이크케이스 -> 카멜케이스 변경
  - MyBaits와 충돌
  - 카멜케이스 적용 후에도 파라미터 변수명 오류

### domain변수명 변경으로 html 변수명 수정 요망

Exception evaluating SpringEL expression

- add, getContent안먹음

### AvoidThrowingRawExceptionTypes

- 가공되지 않은 Exception을 throw하는 것은 비추천
- 어떤 Exception이 적합한지?
  - IllegalArgumentException
  - ![exception](C:\Users\김민식\Pictures\Screenshots\exception.png)

