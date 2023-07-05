# 23-7-05 Oracle on Auzre

### 오라클 데이터베이스 애저에 올리기

### 스크립트 오류 발생시 작업 중단 후 종료 방법

스크립트 시작 부분에 설정함.

\# 오류 발생 시 SQL*Plus를 종료함.(오류 발생 전 변경 내역 commit )

SQL> whenever sqlerror exit sql.sqlcode

\# 오류 발생 시 SQL*Plus를 종료함.(오류 발생 전 변경 내역 rollback)

SQL> whenever sqlerror exit rollback sql.sqlcode

SELECT logging FROM dba_tablespaces WHERE tablespace_name = 'USERS';

```
CREATE INDEX "HFUSR"."ADDITIONAL_CLASS_TYPES_PK_IDX" ON "HFUSR"."DMRS_ADDITIONAL_CT_OBJECTS" ("TYPE_OVID") 
  PCTFREE 10 INITRANS 2 MAXTRANS 255 NOLOGGING COMPUTE STATISTICS NOCOMPRESS LOGGING
  TABLESPACE "USERS" ;
--------------------------------------------------------
--  DDL for Index AGGR_FUNC_DIMENSIONS_FK_IDX
--------------------------------------------------------

  CREATE INDEX "HFUSR"."AGGR_FUNC_DIMENSIONS_FK_IDX" ON "HFUSR"."DMRS_AGGR_FUNC_DIMENSIONS" ("AGGREGATE_FUNCTION_OVID") 
  PCTFREE 10 INITRANS 2 MAXTRANS 255 NOLOGGING COMPUTE STATISTICS NOCOMPRESS LOGGING
  TABLESPACE "USERS" ;
--------------------------------------------------------
--  DDL for Index AGGR_FUNC_LEVELS_FK_IDX
--------------------------------------------------------

  CREATE INDEX "HFUSR"."AGGR_FUNC_LEVELS_FK_IDX" ON "HFUSR"."DMRS_AGGR_FUNC_LEVELS" ("AGGREGATE_FUNCTION_OVID") 
  PCTFREE 10 INITRANS 2 MAXTRANS 255 NOLOGGING COMPUTE STATISTICS NOCOMPRESS LOGGING
  TABLESPACE "USERS" ;
```

SELECT TABLESPACE_NAME,STATUS,CONTENTS FROM DBA_TABLESPACES

`TRI_TBIZPROGRAMEVALITEM_LOG`

### TR_TEMPLOYEE_SSEMPC 문제

### "ORA-00904: "PLS_DECRYPT_B64_ID": 부적합한 식별자
