# java ) 시간 초과

```java
public boolean timeover(String datetime) throws Exception {
		Date current = new java.util.Date();
		String t = datetime;		
		if ( datetime.contains(":") ) {
			t = "";
			for ( String s : datetime.split(":") ) {
				t += s;
			}
		}
		int strLength = t.length();
		if ( strLength < 14 ) {
			int size = 14 - strLength;
			for ( int i = 0 ; i < size ; i++ ) {
				t += "0";				
			}
		}
		Date date = new SimpleDateFormat("yyyyMMddHHmmss").parse(t);
		
		long diff = date.getTime() - current.getTime();
		
		return diff < 0;
		
	}
```

