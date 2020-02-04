# serviceImpl

```java
import java.math.BigDecimal;
import java.util.List;
import java.util.Map;

import org.apache.commons.collections.map.CaseInsensitiveMap;
import org.apache.log4j.Logger;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

import com.fasterxml.jackson.core.type.TypeReference;
import com.fasterxml.jackson.databind.ObjectMapper;

import kr.go.moel.efboard.core.service.managedata.ManageDataService;
import kr.go.moel.efboard.core.service.voice.VoiceService;
import kr.go.moel.efboard.core.util.DateUtility;
import kr.go.moel.efboard.core.adapter.DbmsAdapter;
import kr.go.moel.efboard.core.exception.BusinessLogicException.NextActionType;
import kr.go.moel.efboard.core.manager.ExceptionManager;


@Service
public class CivilComplaintDataServiceImpl implements CivilComplaintDataService {
	
	
	private final Logger logger = Logger.getLogger(getClass());
	
	@Autowired DbmsAdapter dbmsAdapter_backend ;
	@Autowired ExceptionManager exceptionManager;
	@Autowired ManageDataService manageDataService;

/*팝업창 띄우기 > 지방 관서별 민원 처리 현황*/
	@Override
	public Map localCivilComplaintPopup(Map parameter) throws Exception {
		CaseInsensitiveMap resultMap = new CaseInsensitiveMap();
		List list = dbmsAdapter_backend.readList("civilComplaintData.localCivilComplaintPopup", parameter);
		resultMap.put("list", list);
	
		return resultMap;
	}
    
    
    /*팝업_데이터 삭제하기 > 지방 관서별 민원 처리 현황*/
	@Override
	public Map localCivilComplaintPopupDelete(Map parameter) throws Exception {
		CaseInsensitiveMap resultMap = new CaseInsensitiveMap();

		int cnt = dbmsAdapter_backend.transaction("civilComplaintData.localCivilComplaintPopupDelete", parameter);

		if (cnt == 1) {

			resultMap.put("resultCode", "OK");
			resultMap.put("resultMsg", "성공");
		}
		else
			exceptionManager.throwBusinessException("-11", "항목 삭제가 실패하였습니다." , NextActionType.PRINT_END , null);

		return resultMap;
	}
    
    /*팝업창_데이터 등록하기 > 지방 관서별 민원 처리 현황*/
	@Override
	public Map localCivilComplaintPopupRegist(Map parameter) throws Exception {
			CaseInsensitiveMap resultMap = new CaseInsensitiveMap();
			// tbl_mdata_record에 데이터 삽입			
			int cnt = dbmsAdapter_backend.transaction("civilComplaintData.localCivilComplaintPopupRecord", parameter);
			
			//tbl_mdata_record_DATA에 데이터 삽입
			String row_no[] = (String[]) parameter.get("row_no");
			String col_0[]= (String[]) parameter.get("col_0");
			String col_2[]= (String[]) parameter.get("col_2");
			String col_3[]= (String[]) parameter.get("col_3");
			String col_4[]= (String[]) parameter.get("col_4");
			String col_5[]= (String[]) parameter.get("col_5");
			String col_6[]= (String[]) parameter.get("col_6");
	
			for(int i=0; i< row_no.length;i++ ) {
				parameter.put("row_no",row_no[i]);
				parameter.put("col_0",col_0[i]);
				parameter.put("col_2",col_2[i]);
				parameter.put("col_3",col_3[i]);
				parameter.put("col_4",col_4[i]);
				parameter.put("col_5",col_5[i]);
				parameter.put("col_6",col_6[i]);
				cnt = dbmsAdapter_backend.transaction("civilComplaintData.localCivilComplaintPopupRegist", parameter);
			}
			if(cnt > 0 ){
				resultMap.put("resultCode", "OK");
				resultMap.put("resultMsg", "성공");
			} else {
				exceptionManager.throwBusinessException("-11", "정보 등록 실패.", NextActionType.PRINT_END, null);
			}
			return resultMap;
		}
    
    /*팝업창_데이터 수정하기 > 지방 관서별 민원 처리 현황*/
	@Override
	public Map localCivilComplaintPopupModify(Map parameter) throws Exception {
		CaseInsensitiveMap resultMap = new CaseInsensitiveMap();
		int cnt = dbmsAdapter_backend.transaction("civilComplaintData.localCivilComplaintPopupModify", parameter);
		if(cnt == 1){
			resultMap.put("resultCode", "OK");
			resultMap.put("resultMsg", "성공");
		}else{
			exceptionManager.throwBusinessException("-11", "수정 실패.", NextActionType.PRINT_END, null);
		}
		return resultMap;
	}
    
    @Override
    public Map localCivilComplaintPopupSelectBox(Map parameter) throws Exception {        
        CaseInsensitiveMap resultMap = new CaseInsensitiveMap();
        List localCivilComplaintPopupSelectBox = dbmsAdapter_backend.readList("civilComplaintData.localCivilComplaintPopupSelectBox", parameter);
        resultMap.put("localcivilcomplaintpopupselectbox", localCivilComplaintPopupSelectBox);
        
        return resultMap;
    }
}
```

