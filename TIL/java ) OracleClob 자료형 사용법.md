# java ) OracleClob 자료형 사용법

```java
import java.sql.Clob;

public String OracleClob(Map map  , String key) throws Exception {
		if ( map == null ) return "";
		if ( map.get(key) == null ) return "";

		// 해당 map안의 CLOB형 객체를 취득하고
		Clob clob = (Clob) map.get(key);

		// reader를 생성
		Reader reader = clob.getCharacterStream();

		StringBuffer out = new StringBuffer();
		char[] buff = new char[1024];
		int nchars = 0;

		// 스트링 버퍼에 append 시킨후
		while ( (nchars = reader.read(buff)) > 0 ) {
			out.append(buff, 0, nchars);
		}
    
		String result = out.toString();

		reader.close();

		// String형태로 재할당.
		return result;
	}
```

