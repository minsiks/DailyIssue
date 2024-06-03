# 24-5-30 코드 리팩토링 Day 02

## 코드개선

### 1. ImgClctExist 체크

- 기존 코드

  - edge에서 central로 OperatorInspectionData를 리스트로 보내면 img_clct_info테이블에 데이터가 있는지 확인 후 없으면 insert 기능 존재

    - check 로직

    - ```sql
      SELECT COUNT(1) FROM public.img_clct_info_tb 
          	WHERE     img_clct_dtm = #{imgClctDtm} 
          	      AND stckr_id = #{stckrId} 
          	      AND cell_id = #{cellId}
                    AND conr_no = #{conrNo}
                    AND img_taken_dtm = #{imgTakenDtm}
                    AND img_file_nm = #{imgFileNm}
                    AND lot_no = #{lotNo}
                    AND lot_dt = #{lotDt}
                    AND mfact_line_num = #{mfactLineNum}
                    AND line_num = #{lineNum}
      ```

    - 모든 조건이 and 조건으로 묶여 완전히 동일한 data만 조회

### 2. HIST_TABLE 



트랜잭션이 적은게 좋은지 자바 코드가 간결한게 좋은지
