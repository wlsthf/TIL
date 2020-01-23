```java
/**
	 * 기업신청서 상태 변경
	 * @param model
	 * @return
	 * @throws Exception
	 */
	@RequestMapping(value="/updateBizStatus" , method=RequestMethod.POST)
	public void updateBizStatus (Model model)
			throws Exception {
		Map parameter = getParameterMap();



		if(parameter.get("biz_status").equals("3")){}

		Map resultMap = companyService.updateBizStatus(parameter);


		//SMS 발송여부 체크에 따라 SMS 발송
		if(parameter.get("sms_yn") == null){
			///////SMS 통보/////////
			parameter.put("dest_phone", parameter.get("USER_CEL").toString());
			parameter.put("dest_name",  parameter.get("USER_NAME").toString());
			parameter.put("send_phone", "02-3668-0200");
			parameter.put("send_name", "한국예술인복지재단");
			parameter.put("subject", "");
			parameter.put("msg_body", "[예술인복지재단] " + parameter.get("biz_status_txt").toString());


			companyService.insertSmsMsg(parameter);
			///////SMS 통보/////////
		}




		String msg = "";
		String viewName = "getDetailCompanyRequest.ws?biz_quest_idx=" + parameter.get("biz_quest_idx").toString();

		if(resultMap.get("resultCode").toString().equals("1")){
			msg = "승인상태가 정상적으로 변경되었습니다.";
		} else {
			msg = "승인상태 변경 처리중 오류 발생.";
		}


		//WEB FLOW 처리//
		WebFlowTwistBean wtb  = new WebFlowTwistBean();
		wtb.setAlertMsg(msg);
		model.addAttribute(ModelKeyEnum.WEB_FLOW_TWIST.toString() , wtb);
		wtb.setNextActionType(NextActionType.ALERT_AND_MOVE_URL);
		wtb.setNextActionValue(viewName);
		//WEB FLOW 처리//

	}
```

