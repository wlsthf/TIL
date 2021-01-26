# javascript) checked 활용

```javascript

	var $yn				= $("input[name=add_yn]"),
	    $yn2			= $("input[name=add2_yn"),
	    $yn_chk			= $("input[name=add_yn]:checked"),
	    $yn2_chk		= $("input[name=add2_yn]:checked"),
	    $add_content	= $("textarea[name=add_content]");
	
	if ( !$yn.is(":checked") || !$yn2.is(":checked") ) {
		
		alert("yn을 선택해 주세요.");
		$yn.focus();
		return false;
		
	}
	
	if ( $yn_chk.val() == "Y" || $yn2_chk.val() == "Y" ) {
		if ( $add_content.val() == "" ) {
			alert("'예'를 선택한 내용이 있다면 해당사항을 입력해 주시기 바랍니다. ");
			$add_content.focus();
			return false;
		}
		
	}
```

