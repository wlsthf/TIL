```java
/**
	 * 
	 * @param model
	 * @return
	 * @throws Exception
	 */
	@RequestMapping(value="/#####" , method=RequestMethod.POST)
	public void ##### (Model model)
			throws Exception {
		Map parameter = getParameterMap();



		if(parameter.get("####").equals("3")){}

		Map resultMap = #########.#########(parameter);


		//SMS 발송여부 체크에 따라 SMS 발송
		if(parameter.get("###") == null){
			///////SMS 통보/////////
			parameter.put("dest_phone", parameter.get("#").toString());
			parameter.put("dest_name",  parameter.get("##").toString());
			parameter.put("send_phone", "###-####-####");
			parameter.put("send_name", "###");
			parameter.put("subject", "");
			parameter.put("msg_body", "### " + parameter.get("####").toString());


			#######.insertSmsMsg(parameter);
			///////SMS 통보/////////
		}




		String msg = "";
		String viewName = "######?####=" + parameter.get("biz_quest_idx").toString();

		if(resultMap.get("####").toString().equals("1")){
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

