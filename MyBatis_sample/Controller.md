# Controller

```java
@Controller
@RequestMapping(value="/table/")
public class TableController  extends BaseController {
    
	@Autowired ExceptionManager exceptionManager;
	@Autowired TableService tableService; 
    

	@RequestMapping(value="/tableSelect" , method=RequestMethod.GET)
	public String jsp (Model model) throws Exception{		
			Map parameter = getParameterMap(); //웹파라미터	
			Map resultMap = TableService.tableSelect(parameter);
        
			model.addAttribute("list", resultMap.get("list"));
        
			return "tableSelect";
	}
    
    
	@RequestMapping(value="/tableModify", method=RequestMethod.POST)
	public ModelAndView tableModify(
				ModelAndView mav,
				@RequestParam Map<String,Object> parameter
			) throws Exception{
		Map resultMap = TableService.tableModify(parameter);
        
		String msg = "";
        
		if(resultMap.get("resultCode").equals("OK")){
			msg="수정이 완료되었습니다.";
		}else{
			msg="수정이 실패하였습니다.";
		}

		//MODEL에 WEB FLOW 처리 등록	
		mav.addObject(ModelKeyEnum.WEB_FLOW_TWIST.toString() ,
				WebFlowTwistUtility.getInstance(WebFlowTwistBean.NextActionType.ALERT_AND_MOVE_URL, msg, "");		

		return mav;
	}
    
    
	@RequestMapping(value="/tableRegist",method=RequestMethod.POST)
	public ModelAndView tableRegist(
				ModelAndView mav,
				@RequestParam("idx") String row_no[],				
				@RequestParam("col_1")String col_3[],
				@RequestParam("col_2")String col_4[],
				@RequestParam("col_3")String col_5[]		
			) throws Exception{
		Map parameter = new CaseInsensitiveMap();
        
		parameter.put("idx", idx);
        parameter.put("col_1" , col_1);
		parameter.put("col_2" , col_2);
		parameter.put("col_3" , col_3);
		
        // 여려행을 넣는방식에서 사용.. 그냥 써도 바로 넘겨도됨
        
		Map resultMap = TableService.tableRegist(parameter);
		
		String msg = "";
		if(resultMap.get("resultCode").equals("OK")){
			msg = "등록이 완료되었습니다.";
		}else{
			msg = "등록이 실패하였습니다.";
		}
		
		//MODEL에 WEB FLOW 처리 등록	
				mav.addObject(ModelKeyEnum.WEB_FLOW_TWIST.toString() ,
						WebFlowTwistUtility.getInstance(WebFlowTwistBean.NextActionType.ALERT_AND_MOVE_URL, msg, "tableSelect" + parameter.get("idx")));		
				
		return mav;
	}
    
    

	@RequestMapping(value="/tableDelete" , method=RequestMethod.GET)
	public String tableDelete (Model model, @RequestParam Map<String, Object> parameter) throws Exception{		
			Map resultMap = TableService.tableDelete(parameter);

			String msg = "";

			if(resultMap.get("resultCode").equals("OK")) 
				msg = "삭제되었습니다."; 
			else msg = "삭제가 실패하였습니다.";
        
			model.addAttribute("msg",msg);
        
			return "table/tableSelect";
	}       
}
```

