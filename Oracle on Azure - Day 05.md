# 23-8-22 Oracle on Azure Day 05

### 오라클 데이터베이스 애저에 올리기 최종 정리

### 오라클 가상머신 만들기

- Oracle Dababase 19.3.0.0 기준으로 생성
- 보안유형 표준
- 인증형식은 암호로 구성
- OS디스크 표준 HDD로 구성 
- 가상머신이 생성 된 후, 데이터 디스크도 마찬가지로 표준 HDD로 구성 (32GIB)

![2023-08-22 15 20 30](C:\Users\min\Documents\DailyIssue\assets\2023-08-22 15 20 30.png)

### 푸티를 통해 (22번포트) 가상머신에 접근

- 인증형식에서 사용한 아이디랑 비밀번호를 통하여 가상머신에 접근한다

### 가이드에 맞게 데이터베이스 생성

- https://learn.microsoft.com/en-us/azure/virtual-machines/workloads/oracle/oracle-database-quick-create
- https://whiseung.tistory.com/entry/Azure-Oracle-Database19c-%EC%83%9D%EC%84%B1-%ED%9B%84-Azure-Data-FactoryADF-%EC%97%B0%EA%B2%B0

- Azure에서 1521 Oracle 포트 열어둠

TR_TEMPLOYEE_SSEMPC

### 데이터베이스 생성후 테이블 + 유저 생성 데이터 임포트

### 재기동 시 방법

1. Auzre portal에서 가상머신을 재시작.
2. putty 또는 ssh 접근을 통해서 가상머신에 접근
3. sudo su - -> sudo su - oracle 을 하여 오라클로 접속
4. lsnrctl start 를 통해서 수신기 시작
5. sqlplus sys as sysdba 를 입력, sql 로 접속
6. STARTUP 으로 오라클 작동

