# serviceImpl

```java
@Service
public class TableImpl implements TableService {
	
	
	
	@Autowired DbmsAdapter dbmsAdapter_backend ;
	@Autowired ExceptionManager exceptionManager;
	@Autowired ManageDataService manageDataService;

	@Override
	public Map tableSelect(Map parameter) throws Exception {
		CaseInsensitiveMap resultMap = new CaseInsensitiveMap();
		List list = dbmsAdapter_backend.readList("CRUD.tableSelect", parameter);
		resultMap.put("list", list);
	
		return resultMap;
	}
    
    

	@Override
	public Map tableDelete(Map parameter) throws Exception {
		CaseInsensitiveMap resultMap = new CaseInsensitiveMap();

		int cnt = dbmsAdapter_backend.transaction("CRUD.tableDelete", parameter);

		if (cnt == 1) {

			resultMap.put("resultCode", "OK");
			resultMap.put("resultMsg", "성공");
		}
		else
			exceptionManager.throwBusinessException("-11", "항목 삭제가 실패하였습니다." , NextActionType.PRINT_END , null);

		return resultMap;
	}
    

	@Override
	public Map tableRegist(Map parameter) throws Exception {
			CaseInsensitiveMap resultMap = new CaseInsensitiveMap();
        
			// tbl_mdata_record에 데이터 삽입			
			int cnt = dbmsAdapter_backend.transaction("CRUD.tableRegist", parameter);
			
			//tbl_mdata_record_DATA에 데이터 삽입

			String col_1[]= (String[]) parameter.get("col_1");
			String col_2[]= (String[]) parameter.get("col_2");
			String col_3[]= (String[]) parameter.get("col_3");

	
			for(int i=0; i< row_no.length;i++ ) {
				parameter.put("row_no",row_no[i]);
				parameter.put("col_0",col_0[i]);
				parameter.put("col_2",col_2[i]);
				parameter.put("col_3",col_3[i]);
				parameter.put("col_4",col_4[i]);
				parameter.put("col_5",col_5[i]);
				parameter.put("col_6",col_6[i]);
				cnt = dbmsAdapter_backend.transaction("CRUD.tableRegist", parameter);
			}
			if(cnt > 0 ){
				resultMap.put("resultCode", "OK");
				resultMap.put("resultMsg", "성공");
			} else {
				exceptionManager.throwBusinessException("-11", "정보 등록 실패.", NextActionType.PRINT_END, null);
			}
			return resultMap;
		}
    

	@Override
	public Map tableModify(Map parameter) throws Exception {
		CaseInsensitiveMap resultMap = new CaseInsensitiveMap();
		int cnt = dbmsAdapter_backend.transaction("CRUD.tableModify", parameter);
		if(cnt == 1){
			resultMap.put("resultCode", "OK");
			resultMap.put("resultMsg", "성공");
		}else{
			exceptionManager.throwBusinessException("-11", "수정 실패.", NextActionType.PRINT_END, null);
		}
		return resultMap;
	}
    
}
```

