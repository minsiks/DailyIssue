# 23-2-21 Change SpringBoot From Spring- Day 10

### 1. .json, .ajax 확장자 제거하기

2-20 14:03:36.187 [DEBUG] o.s.w.s.m.m.a.RequestResponseBodyMethodProcessor.writeWithMessageConverters : Using 'application/json', given [application/json, text/javascript, */*;q=0.01] and supported [application/json, application/*+json, application/json, application/*+json]

02-20 14:09:16.632 [DEBUG] o.s.w.s.m.m.a.HttpEntityMethodProcessor.writeWithMessageConverters : Using 'application/json', given [application/json, text/javascript, */*;q=0.01] and supported [application/json, application/*+json, application/json, application/*+json]

- 문제 : 확장자 없이는 exception/notfound로 넘어감 (추측 - CustomInterceptor.java에서 validation에서 확인후 넘어가는 듯)
- 해결 : 인터셉터가 가로채서 notfound로 보내는 해당 부분 주석

```java
//				if (menuService.countMenuAuth(menu) == 0
//					&& isAjaxRequest(request) == false && requestUri.indexOf("ajax") == -1 && requestUri.indexOf("json") == -1 
//			    ) {
//			    	// 권한 체크하여 권한이 없으면 permission denied 페이지로
//					log.debug("===============> sendRedirect 2 <=================");
//					System.out.println("@@@@@@@@@@"+isAjaxRequest(request));
//					response.sendRedirect(redirectPermissionDeniedPage);
////					return super.preHandle(request, response, handler);
//					return true;
//				}
```

- 권한체크를 다 지웠는데 이래도 괜찮은지?
- 재 수정!
  - 권한 체크 그대로 가져가고 ajax Send이전에 beforeSend로 AJAX를 헤더에 추가


```js
$.ajax({
			url : "moveAction",
			type : "POST",
			data : param,
			beforeSend: function(xhr) {
				xhr.setRequestHeader("AJAX", "true"); 
			},
			success : function(data) {
				var result = data;
				if (result == "succ") {
					$("#tree").dynatree("getTree").reload();
				} else {
					swal({
				        title: result
				    });
				}
			},
			});
```



### 완료 리스트 (ajax,json 확장자 제거)

- 공통 완료, 상품관리, 상점관리 완료
- 통계, 마이페이지 완료

- 정산 배송, 엑셀 업로드 해결(**HSSFWorkbook** ->**XSSFWorkbook**  변경)

- 주문,회원 관리

> 해결못한 문제 : 

통계,마이페이지,정산,배송,주문,회원 관리 확장자 제거 및 엑셀 업로드(HSSFWorkbook->XSSFWorkbook) 변경
