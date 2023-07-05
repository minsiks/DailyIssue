# 23-7-03 Oracle on Auzre

### 오라클 데이터베이스 애저에 올리기

https://whiseung.tistory.com/entry/Azure-Oracle-Database19c-%EC%83%9D%EC%84%B1-%ED%9B%84-Azure-Data-FactoryADF-%EC%97%B0%EA%B2%B0

### Max_String 사이즈 변경하기 

The error message you received indicates that the ORACLE instance terminated due to a fatal error. Additionally, it mentions that the MAX_STRING_SIZE migration is incomplete.

The ORA-14695 error suggests that the MAX_STRING_SIZE parameter was changed, but the migration process to apply the new setting is incomplete.

To resolve this issue, you can follow these steps:

1. Connect to the database using SQL*Plus or another database administration tool.

2. Start the database instance in upgrade mode by running the following command:

   ```
   sqlCopy code
   STARTUP UPGRADE
   ```

3. Set the MAX_STRING_SIZE parameter to the desired value. For example, to set it to EXTENDED, run the following command:

   ```
   sqlCopy code
   ALTER SYSTEM SET MAX_STRING_SIZE=EXTENDED;
   ```

4. Run the following script to complete the MAX_STRING_SIZE migration:

   ```
   sqlCopy code
   @?/rdbms/admin/utl32k.sql
   ```

5. Shutdown and restart the database:

   ```
   sqlCopy codeSHUTDOWN
   STARTUP
   ```

After completing these steps, the MAX_STRING_SIZE migration should be finalized, and you should be able to use the database without encountering the ORA-14695 error.

If the issue persists or you encounter any other errors, it is recommended to consult the Oracle documentation or contact Oracle Support for further assistance.

```
"
명령의 51,750 행에서 시작하는 중 오류 발생 -
  CREATE INDEX "HFUSR"."ROLE_PROCESSES_FK2_IDX" ON "HFUSR"."DMRS_ROLE_PROCESSES" ("PROCESS_OVID") 
  PCTFREE 10 INITRANS 2 MAXTRANS 255 NOLOGGING COMPUTE STATISTICS NOCOMPRESS LOGGING
  TABLESPACE "USERS"
오류 보고 -
ORA-14102: LOGGING 또는 NOLOGGING 절중 하나만이 지정되어야 합니다
14102. 00000 -  "only one LOGGING or NOLOGGING clause may be specified"
*Cause:    LOGGING was specified more than once, NOLOGGING was specified
           more than once, or both LOGGING and NOLOGGING were specified.
*Action:   Remove all but one of the LOGGING or NOLOGGING clauses and
           reissue the statement.

명령의 51,743 행에서 시작하는 중 오류 발생 -
CREATE INDEX "HFUSR"."ROLE_PROCESSES_FK1_IDX" ON "HFUSR"."DMRS_ROLE_PROCESSES" ("ROLE_OVID") 
  PCTFREE 10 INITRANS 2 MAXTRANS 255 NOLOGGING COMPUTE STATISTICS NOCOMPRESS LOGGING
  TABLESPACE "USERS"
오류 보고 -
ORA-14102: LOGGING 또는 NOLOGGING 절중 하나만이 지정되어야 합니다
14102. 00000 -  "only one LOGGING or NOLOGGING clause may be specified"
*Cause:    LOGGING was specified more than once, NOLOGGING was specified
           more than once, or both LOGGING and NOLOGGING were specified.
*Action:   Remove all but one of the LOGGING or NOLOGGING clauses and
           reissue the statement.

명령의 51,750 행에서 시작하는 중 오류 발생 -
  CREATE INDEX "HFUSR"."ROLE_PROCESSES_FK2_IDX" ON "HFUSR"."DMRS_ROLE_PROCESSES" ("PROCESS_OVID") 
  PCTFREE 10 INITRANS 2 MAXTRANS 255 NOLOGGING COMPUTE STATISTICS NOCOMPRESS LOGGING
  TABLESPACE "USERS"
오류 보고 -
ORA-14102: LOGGING 또는 NOLOGGING 절중 하나만이 지정되어야 합니다
14102. 00000 -  "only one LOGGING or NOLOGGING clause may be specified"
*Cause:    LOGGING was specified more than once, NOLOGGING was specified
           more than once, or both LOGGING and NOLOGGING were specified.
*Action:   Remove all but one of the LOGGING or NOLOGGING clauses and
           reissue the statement.

명령의 51,757 행에서 시작하는 중 오류 발생 -
  CREATE INDEX "HFUSR"."ROLES_PK_IDX" ON "HFUSR"."DMRS_ROLES" ("ROLE_OVID") 
  PCTFREE 10 INITRANS 2 MAXTRANS 255 NOLOGGING COMPUTE STATISTICS NOCOMPRESS LOGGING
  TABLESPACE "USERS"
오류 보고 -
ORA-14102: LOGGING 또는 NOLOGGING 절중 하나만이 지정되어야 합니다
14102. 00000 -  "only one LOGGING or NOLOGGING clause may be specified"
*Cause:    LOGGING was specified more than once, NOLOGGING was specified
           more than once, or both LOGGING and NOLOGGING were specified.
*Action:   Remove all but one of the LOGGING or NOLOGGING clauses and
           reissue the statement.

명령의 51,764 행에서 시작하는 중 오류 발생 -
  CREATE INDEX "HFUSR"."ROLES_FK_MODEL_IDX" ON "HFUSR"."DMRS_ROLES" ("MODEL_OVID") 
  PCTFREE 10 INITRANS 2 MAXTRANS 255 NOLOGGING COMPUTE STATISTICS NOCOMPRESS LOGGING
  TABLESPACE "USERS"
오류 보고 -
ORA-14102: LOGGING 또는 NOLOGGING 절중 하나만이 지정되어야 합니다
14102. 00000 -  "only one LOGGING or NOLOGGING clause may be specified"
*Cause:    LOGGING was specified more than once, NOLOGGING was specified
           more than once, or both LOGGING and NOLOGGING were specified.
*Action:   Remove all but one of the LOGGING or NOLOGGING clauses and
           reissue the statement.

명령의 51,771 행에서 시작하는 중 오류 발생 -
  CREATE INDEX "HFUSR"."ROLLUP_LINK_ATTRS_FK_IDX" ON "HFUSR"."DMRS_ROLLUP_LINK_ATTRS" ("ROLLUP_LINK_OVID") 
  PCTFREE 10 INITRANS 2 MAXTRANS 255 NOLOGGING COMPUTE STATISTICS NOCOMPRESS LOGGING
  TABLESPACE "USERS"
오류 보고 -
ORA-14102: LOGGING 또는 NOLOGGING 절중 하나만이 지정되어야 합니다
14102. 00000 -  "only one LOGGING or NOLOGGING clause may be specified"
*Cause:    LOGGING was specified more than once, NOLOGGING was specified
           more than once, or both LOGGING and NOLOGGING were specified.
*Action:   Remove all but one of the LOGGING or NOLOGGING clauses and
           reissue the statement.
"
There are so many of these that I can't modify them one by one. Can't I change the settings at once? And it works well in other configuration settings, but in which environment is the query statement applied? Now I'm using Oracle 19c.
```

