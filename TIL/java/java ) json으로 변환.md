# java ) json으로 변환

```java
public String toJson(Map map, String ... value) {
		int length = value.length;
		JSONObject json = new JSONObject();
		
		for ( int i = 0 ; i < length ; i++ ) {
			try {
				json.put(value[i], nvl(map, value[i]));
			} catch(JSONException e) {}
		}
		return json.toString();
	}
```

