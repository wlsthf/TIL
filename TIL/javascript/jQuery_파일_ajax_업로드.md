# jQuery) 파일 ajax 업로드



```javascript
	function uploadFile() {
		var filePath = $("#file").val();
		var ext = getExtFromFilePath(filePath);
		
		var formData = new FormData($('#fileFrm')[0]);
		
		$.ajax({ 
			type: "POST", 
			enctype: 'multipart/form-data', // 필수 
			url: '주소', 
			data: formData, // 필수 
			processData: false, // 필수 
			contentType: false, // 필수 
			cache: false, 
			success: function (data) {
				console.log(data)
			}, 
			error: function (e) {
				console.log(e);
			} 
		});
	}
```

