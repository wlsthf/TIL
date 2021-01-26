# jQuery) ajax로 List 보내기



```javascript
function upload() {
	var de_arr		 = new Array(),
		time_arr	 = new Array(),
		value_arr	 = new Array();
	
	for ( var i = 0; i < data.items.length; i++ ) {
		de_arr.push(data.items[i].de.replace(/-/g, ""));
		time_arr.push(data.items[i].time.replace(":", ""));
		value_arr.push(data.items[i].value);
	}
	
	var jsonData = {
		"de_arr"		: de_arr,
		"time_arr"		: time_arr,
		"value_arr"		: value_arr,
		"user_no"		: $("input[name=user_no]").val(),
	};
	
	$.ajax({ 
		type		: "POST", 
		url			: '유알엘을 입력하세요!',
		dataType	: "JSON",
		data		: jsonData, 
		success		: function (data) {
			console.log(data);
			alert(data.resultmsg);
			opener.location.reload();
			window.close();
		}, 
		error		: function (e) {
			console.log(e);
		},		
		// 로딩 표시
		beforeSend	: function() {
			로딩.show();
		}, 
		// 완료시 로딩창 제거
		complete	: function() {
			로딩.hide();
		} 
	});
}
```



요런식으로 list로 만들어서 보내거나 form을 만들어서 보낸다!

=> de_arr[] 의 이름으로 받아서 split 하여 사용하면 됨 ( 마지막에 , 없음! )

