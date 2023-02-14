# 23-2-14 Change SpringBoot From Spring- Day 06

### Admin 상점관리 spring->springboot 고도화

#### 1. 주문내역 관리

- c:set 타임리프 대체제 
  - with으로는 지역변수로밖에 선언 불가

  - 알고리즘 분석

  - ex_ 만약에 java라면 c:forEach와 c:set등 jstl,html을 자바 코드로 변환 해석

    ```java
    int current = 0;
    int num = 0;
    int rowspan = 0;
    
    List<OrderInfoMgmt> orderInfoList = orderListService.getOrderInfoList(orderInfoMgmt);
    List<String> rowCounts = orderListService.getOrderRowCount(orderInfoMgmt);
    
    for(int i = 0; i<orderInfoList.size(); i++){
        if(current == 0){
            rowspan = rowCount.get(num); // 해당 중복 주문번호 개수를 구해, rowspan을 구함
            current = rowCount.get(num);
            num = num+1;
        }
        current = current-1;
    }
    ```

  - 타임리프 th:with를 사용하여 중복 제거까지

  - 참고 : https://papababo.tistory.com/entry/themeleaf-foreach%EC%8B%9C-%EC%9D%B4%EC%A0%84%EC%95%84%EC%9D%B4%ED%85%9C%EA%B3%BC-%ED%98%84%EC%9E%AC%EC%95%84%EC%9D%B4%ED%85%9C-%EB%B9%84%EA%B5%90%ED%95%98%EA%B8%B0

  - 

> 해결못한 문제 : 
>
> 1. 엑셀 다운로드 : JSP에서도 기능 X  
>
> 1. 팝업 타임리프에서는 잘뜨는데 jsp에서는 안뜨는 현상
>
> 1. 딜리버리 트래킹 종료된 키 값
>
>    DeliveryCode.java에서
>
>    private String t_key = "ZBDehDj92gWtK79HITajgA";
>
>    ```xml
>    <Result>
>    <status>false</status>
>    <message>키 정보를 찾을수 없습니다. 종료된 키 or 유효하지 않은 키입니다.</message>
>    <Code>101</Code>
>    </Result>
>    ```
>
> 4. paging count 18인데 1개 ??
