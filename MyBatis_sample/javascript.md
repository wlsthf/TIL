# javascript

```javascript
// 데이터 변경
function modifyData(idx, column_name, data){
	
	var popUrl = 'tableModify?idx='+idx+'&row_no='+row_no+'&data='+data+'&column_name='+column_name;	
	
	var offset = $("#regist_form").offset();
	
	var top = offset.top;
	var left = offset.left;
	
	var popOption = "width=350, height=110, top="+top+", left="+left+", resizable=yes, scrollbars=yes, status=no, menubar=no, toolbar=no, location=no;";    //팝업창 옵션(optoin)
	
	chkPopup = window.open(popUrl,"y",popOption);	
}

$(function(){
    // 데이터 등록
    $("#regist_btn").click(function(){
		if(confirm('등록 하시겠습니까?')) {
			$("#regist_form").prop("action", "tableResist");
    		$("#regist_form").submit();
		}
	});
    
    
    // 데이터 삭제
    function delRowAjax(record_id, row_no){
        
		var result = confirm("데이터를 삭제 하시겠습니까? 삭제 후에는 복구가 불가능 합니다.");
	
	if(result){
		$.ajax({
		    type: "get",
		    url: "tableDelete",
		    data: {idx	: idx},
		    dataType: "json",
		    success:function(result) {
		    	alert(result);
			} 
		});		
	}
   
    $(".delRowData").live("click", function(){
        $(this).parent().parent().remove();		
	}); 
)};    
```

