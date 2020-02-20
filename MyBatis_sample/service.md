# service

```java
import java.util.Map;

public interface TableService {
	
	Map tableSelect(Map parameter) throws Exception;
	Map tableDelete(Map parameter) throws Exception;
	Map tableRegist(Map parameter) throws Exception;
	Map tableModify(Map parameter) throws Exception;	
}
```

