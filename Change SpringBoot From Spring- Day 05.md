# 23-2-13 Change SpringBoot From Spring- Day 05

### Admin 상점관리 spring->springboot 고도화

### 1. 일별정산 관리 ListAction 미출력 오류

- 타임리프 문법 문제. 
  - th:text가 붙으면 태그안에 text를 붙일수 없음

#### 2. 건별정산 관리 팝업

- th:onclick 변수 오류 

  - `th:onclick="javascript:openModal('/admin/order/orderList/detailPopup.ajax' , 'orderDetailPopup' , 'order_seq=[[${info.order_seq}]]' , '900');"`

  - 원인 : onclick에 [[${info.order_seq}]]로 담아 함수를 호출하면 "" <- 따옴표가 같이 Controller단으로 같이 전송되는 오류

  - 해결: `th:onclick="javascript:calculDetailAction([[${info.calcul_seq}]])" `

    - for문으로 돌아가는 각 info의 번호 값을 파라미터로 보내주어 함수내 변수로 받아서 openModal해주어 해당 오류를 해결

  - ```javascript
    function calculDetailAction(calculSeq){
    		openModal('./calculDetailPopup.ajax' , 'calculDetailPopup' , {calcul_seq :calculSeq}, '700');
    	}
    ```

- openModal : orderDetailPopup 보류 orderList 고도화 할때 수정

#### 3. 배송관리

- Product Detail팝업 실행 안됨
  - 원인 : html파일 부재
- delivery_tracking 키값 안맞아 사용 불가
  - `javascript:delivery_tracking('${info.echn_waybil_no}')`
  - null값이라 t_invoice 추적 불가, if문으로 막아놓지 않은 이유?

#### 4. 주문내역 관리

- c:set 타임리프 대체제 
  - with으로는 지역변수로밖에 선언 불가

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
>    
