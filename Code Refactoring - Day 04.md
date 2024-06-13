# 24-6-12 코드 리팩토링 Day 04

## xrayImageFileNameRegx Test

1. STACK_ID

   - 테스트 케이스 (정상 : Xray_G6037D7CP7610077_20230713000002_**Stack02** VISION2__.bmp)

     - INTERNAL_ERROR (FILE NAME IS INVALID)

       > file1 에러시 2파일 전체 저장 X

       - Sdd02
       - D#DDDD
       - Stack_1

     -  OK

       - 2345021
       - DDDDDD
2. cellId

   1. 테스트 케이스 (Xray\_**G6037D7CP7610077**_20230713000002_Stack02 VISION2__.bmp)

      - INTERNAL_ERROR (FILE NAME IS INVALID)

        > file1 에러시 2파일 전체 저장 X

        - A12345ABC1B23456
        - g6037D7CP7610077

3. IMG_TAKEN_DTM

   1. 테스트 케이스 (Xray\_G6037D7CP7610077_20230713000002_Stack02 VISION2__.bmp)

   fff

