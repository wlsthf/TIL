# input value check

```javascript
function numCheck(event) { 
		  var eventReference = (typeof evt !== "undefined")? evt : event;
		  var eventTarget = 
			  (typeof eventReference.target !== "undefined")? eventReference.target : eventReference.srcElement;
		  
		  var inputVal = eventTarget.value;
		  eventTarget.value = inputVal.replace(/[^0-9]/gi,'');
	//	  eventTarget.value = inputVal.replace(/^\d*[.]\d{5}$/gi,'');
	}
	function engCheck(event) { 
		  var eventReference = (typeof evt !== "undefined")? evt : event;
		  var eventTarget = 
			  (typeof eventReference.target !== "undefined")? eventReference.target : eventReference.srcElement;
		
	
	   	  var inputVal = eventTarget.value;
	   	  eventTarget.value = inputVal.replace(/[^a-z0-9]/gi,'');    
		
	}
	function korCheck(){
		$(this).val($(this).val().replace( /[ㄱ-ㅎ|ㅏ-ㅣ|가-힣]/g, '' ) );
	}
		
	function chkNum(val){
		var chk_num = val;
		if($.isNumeric(chk_num) == false){
			return false;
		} else {
			return true;
		}
	}
```

