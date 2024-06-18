# 24-6-14 코드 리팩토링 Day 06

## 이미지 센트럴 전송 변경

- AI 센트럴 전송
  - AI_INSP_RSLT_HIST_TB 과 조인해서 수집
  - AI판정은 1번만
  - 정의서 규격대로 
  - Hitmap 추가

> 1. insertAiInspectHistoryList (IMG_INSP_RSLT_SEND_HST_TB에 AI 전송 시)
>
> - ai전송시 쿼리 중 RGSTR_ID 를 어떻게 설정 `operator는 opertrEmpNum을 입력
>- dsf
