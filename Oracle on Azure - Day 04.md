# 23-7-05 Oracle on Auzre

### 오라클 데이터베이스 애저에 올리기

### 데이터 디스크 교체

```dbca -silent \    -createDatabase \    -templateName General_Purpose.dbc \    -gdbname new_oratest1 \    -sid oratest1 \    -responseFile NO_VALUE \    -characterSet AL32UTF8 \    -sysPassword OraPasswd1 \    -systemPassword OraPasswd1 \    -createAsContainerDatabase false \    -databaseType MULTIPURPOSE \    -automaticMemoryManagement false \    -storageType FS \    -datafileDestination "/u02/oradata/" \    -ignorePreReqs
```

dbca -silent \    -createDatabase \    -templateName General_Purpose.dbc \    -gdbname oratest \    -sid oratest \    -responseFile NO_VALUE \    -characterSet AL32UTF8 \    -sysPassword OraPasswd1 \    -systemPassword OraPasswd1 \    -createAsContainerDatabase false \    -databaseType MULTIPURPOSE \    -automaticMemoryManagement false \    -storageType FS \    -datafileDestination "/u02/oradata/" \    -ignorePreReqs
