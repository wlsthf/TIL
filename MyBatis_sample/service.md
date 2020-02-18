# service

```java
import java.util.Map;

public interface CivilComplaintDataService {
	
	//팝업 > 지방 관서별 민원 처리 현황
	Map localCivilComplaintPopup(Map parameter) throws Exception;
	Map localCivilComplaintPopupDelete(Map parameter) throws Exception;
	Map localCivilComplaintPopupRegist(Map parameter) throws Exception;
	Map localCivilComplaintPopupModify(Map parameter) throws Exception;
    Map localCivilComplaintPopupSelectBox(Map parameter) throws Exception;
	
}
```

