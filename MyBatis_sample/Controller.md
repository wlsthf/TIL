# Controller

```java
@Controller
@RequestMapping(value="/civilComplaintData/")
public class CivilComplaintDataController  extends BaseController {
    
	@Autowired ExceptionManager exceptionManager;
	@Autowired CivilComplaintDataService civilComplaintDataService; 
    
    /*팝업 리스트 > 지방관서별 민원 처리 현황*/
	@RequestMapping(value="/localCivilComplaintPopup" , method=RequestMethod.GET)
	public String localCivilComplaintPopup (Model model) throws Exception{		
			Map parameter = getParameterMap(); //웹파라미터	
			Map resultMap = civilComplaintDataService.localCivilComplaintPopup(parameter);
			model.addAttribute("list", resultMap.get("list"));
			return "civilComplaintData/localCivilComplaintPopup.empty";
	}
    
    /*팝업 데이터 하나 가져오기 > 지방관서별 민원 처리 현황*/
	@RequestMapping(value="/localCivilComplaintPopupModify" , method=RequestMethod.GET)
	public String localCivilComplaintPopupModify (Model model)
			throws Exception {

		Map parameter = getParameterMap(); //웹파라미터

		Map resultMap = civilComplaintDataService.localCivilComplaintPopupSelectBox(parameter);
		
		model.addAttribute("list", resultMap.get("localcivilcomplaintpopupselectbox"));

		return "civilComplaintData/localCivilComplaintPopupModify.empty";
	}
	
	/*팝업 데이터 수정 > 지방관서별 민원 처리 현황*/
	@RequestMapping(value="/localCivilComplaintPopupModify", method=RequestMethod.POST)
	public ModelAndView localCivilComplaintPopupModify(
				ModelAndView mav,
				@RequestParam Map<String,Object> parameter
			) throws Exception{
		Map resultMap = civilComplaintDataService.localCivilComplaintPopupModify(parameter);
		String msg = "";
		if(resultMap.get("resultCode").equals("OK")){
			msg="수정이 완료되었습니다.";
		}else{
			msg="수정이 실패하였습니다.";
		}

		//MODEL에 WEB FLOW 처리 등록	
		mav.addObject(ModelKeyEnum.WEB_FLOW_TWIST.toString() ,
				WebFlowTwistUtility.getInstance(WebFlowTwistBean.NextActionType.ALERT_AND_MOVE_URL, msg, ""));		

		return mav;
	}
    
    /*팝업 등록 > 지방관서별 민원 처리 현황*/
	@RequestMapping(value="/localCivilComplaintPopupRegist",method=RequestMethod.POST)
	public ModelAndView localCivilComplaintPopupRegist(
				ModelAndView mav,
				@RequestParam("row_no") String row_no[],				
				@RequestParam("cv_note") String col_0[],
				@RequestParam("cv_value")String col_2[],
				@RequestParam("col_3")String col_3[],
				@RequestParam("col_4")String col_4[],
				@RequestParam("col_5")String col_5[],
				@RequestParam("col_6")String col_6[]		
			) throws Exception{
		Map parameter = new CaseInsensitiveMap();
		parameter.put("row_no", row_no);
		parameter.put("col_0" , col_0);
		parameter.put("col_2" , col_2);
		parameter.put("col_3" , col_3);
		parameter.put("col_4" , col_4);
		parameter.put("col_5" , col_5);
		parameter.put("col_6" , col_6);
		Map resultMap = civilComplaintDataService.localCivilComplaintPopupRegist(parameter);
		
		String msg = "";
		if(resultMap.get("resultCode").equals("OK")){
			msg = "등록이 완료되었습니다.";
		}else{
			msg = "등록이 실패하였습니다.";
		}
		
		//MODEL에 WEB FLOW 처리 등록	
				mav.addObject(ModelKeyEnum.WEB_FLOW_TWIST.toString() ,
						WebFlowTwistUtility.getInstance(WebFlowTwistBean.NextActionType.ALERT_AND_MOVE_URL, msg, "localCivilComplaintPopup"));		
				
		return mav;
	}
    
    /*지방관서 select box ajax*/
    @RequestMapping(value="/localCivilComplaintPopupSelectBox" , method=RequestMethod.GET)   
    public String localCivilComplaintPopupSelectBox (Model model) throws Exception{
        Map parameter = getParameterMap(); //웹파라미터  
        Map resultMap = civilComplaintDataService.localCivilComplaintPopupSelectBox(parameter);
        model.addAttribute("jsonDataMap" , resultMap.get("localcivilcomplaintpopupselectbox"));
        return "jsonFromMapStandardView"; //json 출력 view로 리턴
    }
    
    /*팝업 삭제 > 지방관서별 민원 처리 현황*/
	@RequestMapping(value="/localCivilComplaintPopupDelete" , method=RequestMethod.GET)
	public String localCivilComplaintPopupDelete (Model model, @RequestParam Map<String, Object> parameter) throws Exception{		
			Map resultMap = civilComplaintDataService.localCivilComplaintPopupDelete(parameter);

			String msg = "";

			if(resultMap.get("resultCode").equals("OK")) 
				msg = "삭제되었습니다."; 
			else msg = "삭제가 실패하였습니다.";
			model.addAttribute("msg",msg);
			return "civilComplaintData/localCivilComplaintPopup.empty";
	}
    
    
    
}
```

