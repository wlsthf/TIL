# javascript ) 첨부파일 관련

```javascript
	//첨부파일 용량확인 및 용량표시
	$("input[type=file]").change(function(){
		var $target = $(this);				
		var $file_size = $target.parent().find(".file_size");	//파일용량표시 위치
		var $btn_delete = $target.parent().find(".file_delete");		//파일삭제버튼 위치
		
		
		var is_fail = false;
		

		if( $target.val() != ""){
			var fileSize = this.files[0].size;
			var maxSize = 50 * 1024 * 1024;

// 			//파일용량 변수에 담기
// 			if(target == "file1"){
// 				chk_file1_size = fileSize;
// 				chk_file1 = this.files[0].name;
// 			} else if(target == "file2"){
// 				chk_file2_size = fileSize;
// 			}

			//파일용량 체크
			if( fileSize > maxSize ){
				alert("첨부파일는 최대 50MB까지 첨부 가능합니다.");
				is_fail = true;
			}

			
			
			if ( !is_fail ) {
			
				//파일용량 표시
				iSize = fileSize / 1024;
				if(iSize / 1024 > 1){
					iSize = (Math.round((iSize/1024)*100)/100);
					$file_size.html("(" + iSize + "MB)");
					$btn_delete.show();
				} else {
					iSize = (Math.round(iSize * 100) / 100);
					$file_size.html("(" + iSize + "KB)");
					$btn_delete.show();
				}
				
			}
		}



		var file_name = this.files[0].name,
			file_len = file_name.length,
			ext = file_name.substring(file_name.lastIndexOf('.')+1, file_len).toLowerCase(),
			chk_file_name = file_name.substring(0, file_name.lastIndexOf('.'));


		//확장자 체크
		if( ext != "jpg" && ext != "jpeg" && ext != "png" &&  ext != "gif" &&  ext != "bmp" &&  ext != "pdf" &&
			ext != "hwp" && ext != "xls" && ext != "xlsx" &&  ext != "ppt" &&  ext != "pptx" &&  ext != "doc" &&  ext != "docx" &&  ext != "zip"	){
			alert("첨부파일은 (jpg, jpeg, png, gif, bmp, pdf, hwp, xls, xlsx, ppt, pptx, doc, docx, zip) 형식만 등록 가능합니다.");
			$btn_delete.click();
			return false;
		}
		
		$target.parent().find(".chk_del").val("");
		
	});

	
	
	
	// 파일삭제 버튼 클릭
	$(".file_delete").click(function(){
		
		var $this = $(this);
		var $tg = $this.parent();
		
		$tg.find("input[type=file]").val("");
		$tg.find("input[type=file]").show();
		$tg.find(".file_area").html("");
		$tg.find(".file_size").html("");
		$tg.find(".chk_del").val("del");
		$this.hide();
	});
```

