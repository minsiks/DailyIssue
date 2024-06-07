# 24-6-03 코드 리팩토링 Day 03

## 코드개선

### 1. imgSt필드 누락 (AI판정시 & collect이미지 insert시)

### 2. Image Insert 시 registId 필드 누락

### 3. 작업자 판정 결과 삽입시 OPERTR_INSP_NG_CL_CD null값 Insert

- 기존에는 없으면 ''로 insert

### 2. edge ui 판정결과 변경시 last_upd_dtm 변경 X

- updateOperatorInspection 쿼리

