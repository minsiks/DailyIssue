# 24-5-27 코드 리팩토링 Day 01

## 코드개선

### 작업자 체크

- 기존 코드

```java
public static boolean checkOperator(Map<String, Object> operatorMap) {
	    // OperatorMap이 null인 경우 유효하지 않음
	    if (operatorMap == null) {
	        return false;
	    }

	    String imgCnt = (String) operatorMap.get("IMG_CNT");
	    String[] requiredKeys = new String[0];

	    if ("1".equals(imgCnt)) {
	        requiredKeys = new String[] {
	            "FILE1",
	            "FILE_NAME1",
	            "IMG_CNT"
	        };
	    } else if ("2".equals(imgCnt)) {
	        requiredKeys = new String[] {
	        		"FILE1",
		            "FILE_NAME1",
		            "FILE2",
		            "FILE_NAME2",
		            "IMG_CNT"
	        };
	    }else if ("3".equals(imgCnt)) {
	    	requiredKeys = new String[] {
	        		"FILE1",
		            "FILE_NAME1",
		            "FILE2",
		            "FILE_NAME2",
		            "FILE3",
		            "FILE_NAME3",
		            "IMG_CNT"
	        };
		}

	    // 모든 필수 키가 OperatorMap에 포함되어 있는지 확인
	    for (String key : requiredKeys) {
	        if (!operatorMap.containsKey(key)) {
	            return false;
	        }
	    }
	    return true;
	}
```

- 개선 코드

```java
public static boolean checkOperator2(Map<String, Object> operatorMap) {
	    // OperatorMap이 null인 경우 유효하지 않음
	    if (operatorMap == null) {
	        return false;
	    }

	    List<String> requiredKeysList = new ArrayList<>();
	    
	   for (int i = 1; i <= (int) operatorMap.get("IMG_CNT"); i++) {
		   requiredKeysList.add("FILE" + i);
		   requiredKeysList.add("FILE_NAME" + i);
	   }	    	
	   requiredKeysList.add("IMG_CNT");
	    
	    return requiredKeysList.stream()
	    	    .allMatch(operatorMap::containsKey);
	}
```

### 

cnetral 작업자 30초마다 받고 
