# javascript

```javascript
// 데이터 변경
function modifyData(record_id, row_no, data, column_name, col_0){	
	var popUrl = 'localCivilComplaintPopupModify?record_id='+record_id+'&row_no='+row_no+'&data='+data+'&column_name='+column_name+'&local_name='+col_0;	
	
	var offset = $("#regist_form").offset();
	
	var top = offset.top;
	var left = offset.left;
	
	var popOption = "width=350, height=110, top="+top+", left="+left+", resizable=yes, scrollbars=yes, status=no, menubar=no, toolbar=no, location=no;";    //팝업창 옵션(optoin)
	
	chkPopup = window.open(popUrl,"y",popOption);	

}
$(function(){
    $("#columnBody").on("paste", "textarea", function(e){
		var $this = $(this);
		var rowoffset = $this.parent().parent().index();
		var coloffset = $this.parent().index();
	   $this.val("");
		setTimeout(function(){
		    var pastedValue=$.trim($this.val());
		    if (pastedValue.indexOf("\n")>0 || pastedValue.indexOf("\t")>0  ) {
		        var rows = pastedValue.split("\n");
		        
		        for (var i=0;i<rows.length;i++) {
		            var columns = rows[i].split("\t");
		            for (var j=0;j<columns.length;j++) {
		                var column = $.trim(columns[j]);
		                console.log(i+" - "+j+" : "+column);
		                if (column) $("#columnBody").find("tr:nth-child("+(i+1+rowoffset)+")").find("th:nth-child("+(j+1+coloffset)+")").find("textarea").val(column);
		            }
		        }	    	
		    }
		}, 10);
	});
	$("#regist_btn").click(function(){

		if($(".cv_note").val() == ""){
			alert("지청을 입력하세요.");
			return
		}
		if($(".cv_value").val() == ""){
			alert("지방 관서를 입력하세요.");
			return;
		}
		if(confirm('관리데이터를 등록 하시겠습니까?')) {
			$("#regist_form").prop("action", "localCivilComplaintPopupRegist");
    		$("#regist_form").submit();
		}
		
	});
	
	$("#apply_btn").click(function(){
		if(confirm('차트데이터에 적용 하시겠습니까?')) {
			$("#regist_form").prop("action", "localCivilComplaintApply");
    		$("#regist_form").submit();
		}
	});

	//초기화
	$("#btn_reset").click(function(){
			$("#regist_form")[0].reset();		
	});
	
	$("#btn_list").click(function(){
		location = 'list?user_code=${user_code}';
	});
	function itoStr($num)
    {
        $num < 10 ? $num = '0'+$num : $num;
        return $num.toString();
    }
     
    $('#btnExport').on('click', function () {
        var dt = new Date();
        var year =  itoStr( dt.getFullYear() );
        var month = itoStr( dt.getMonth() + 1 );
        var day =   itoStr( dt.getDate() );
        var hour =  itoStr( dt.getHours() );
        var mins =  itoStr( dt.getMinutes() );
		var title = '${schema.list[0].mng_data_title }';
        var postfix = year + month + day + "_" + hour + mins;
        var fileName = title + "_"+ postfix + ".xls";
        
        var tblId = 'tblExport';
        
        var uri = $("#"+tblId).excelexportjs({
            containerid: tblId
            , datatype: 'table'
            , worksheetName:title
            , returnUri:true
        });

        $(this).attr('download', fileName).attr('href', uri).attr('target', '_blank');
    });

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
	
	function modifyData(row_idx, row_key, schema_idx, item){
		var type;
	
		$.ajax({
			type: 'get',
			url: 'getSchemaType',
			data:
			{
				"schema_idx":schema_idx
			},
			dataType: 'json',
			error:function(x,e){
				console.log(x);
				console.log(e);
				alert("오류가 발생하였습니다.");
			},
			success: function (data) {
				
				var code_value = data.column[0].code_value;
				var type = data.column[0].column_type;
				var length = data.column[0].column_length;
				
				if(code_value == 'MNG_TYPE_NUMBER'){
					type='num';
				}else if(code_value == 'MNG_TYPE_TEXT'){
					type='text';
				}else if(code_value == 'MNG_TYPE_input'){
					type='input';
				}
				
				var popUrl = 'modifyDataPopup?row_idx='+row_idx+'&row_key='+row_key+'&schema_idx='+schema_idx+'&input_data='+item+'&type='+type+'&length='+length;	
				
				var offset = $("#regist_form").offset();
				
				var top = offset.top;
				var left = offset.left;
				
				var popOption = "width=300, height=110, top="+top+", left="+left+", resizable=yes, scrollbars=yes, status=no, menubar=no, toolbar=no, location=no;";    //팝업창 옵션(optoin)
				
				chkPopup = window.open(popUrl,"y",popOption);	
				
				
			}
		});	
		
	}
	
	function getModifyData(row_idx, row_key, schema_idx, input_data){
		
		$.ajax({
			type: 'get',
			url: 'modifyData',
			data:
			{
				"row_idx":row_idx,
				"row_key":row_key,
				"schema_idx":schema_idx,
				"input_data":input_data
			},
			dataType: 'json',
			error:function(x,e){
				console.log(x);
				console.log(e);
				alert("수정 도중 오류가 발생하였습니다.");
			},
			success: function (data) {
				$("#"+row_idx).text(input_data);
				if(row_idx=="")
					 location.reload();
				
				alert("수정 되었습니다.");
			}
		});
		
	}
	
	
	function pasteData(items, x, y){
	
		var columnList = new Array();
		var inputColumnList = new Array();
	
		<c:forEach items="${schema.columnlist}" var="column">
			columnList.push('${column.mng_data_schema_idx}');
		</c:forEach>
	
		
		 for (i=0 ; i < columnList.length; i++){
			  inputColumnList.push(document.getElementsByName(columnList[i]));
		  }
		 
		 
	    // split into rows
	    items = items.trim();
	
		var rows= items.split('\n');
		for (i=0; i<rows.length; i++){
			var columns = rows[i].split('\t');
			for(j=0; j<columns.length; j++){
				inputColumnList[j+x][i+y].value=columns[j];
			}
		}
	}
	
	//스키마 추가 클릭시 TR 추가
	$("#addRow_1").live("click", function() {
		var rowcnt = $("#addRowCnt_1").val();	//추가될 행 개수
		var row_no = Number($('.row_no').last().val()) + 1;
		if(isNaN(row_no)) {
			row_no = 0; 
		}
		if(rowcnt=='' || rowcnt==0)
			rowcnt=1;
		
		for(i = 0 ; i<rowcnt ; i++){
			addRow = '<tr id="">';
			addRow += '<input type="hidden" name="row_no" class="row_no" value="'+row_no+'">';			
			addRow += '<th style="padding:0px 0px 0px 0px;">' +
			'<select name="cv_note" class="cv_note" style="width:100px;">' +
				'<option value="">지방청</option>' +
				'<option value="12010">서울청</option>' +
				'<option value="13000">부산청</option>' +
				'<option value="14010">대구청</option>' +
				'<option value="15000">중부청</option>' +
				'<option value="16000">광주청</option>' +
				'<option value="17000">대전청</option>' +
			'</select></th>';
			addRow += '<th ><select name="cv_value" class="cv_value" ><option value="">지방관서</option></select></th>';
			     
			addRow += '<th style="padding:0px 0px 0px 0px;"><textarea name="col_3" style="width:100px; text-align:center; padding:5px; height: 15px;"></textarea></th>';
			addRow += '<th style="padding:0px 0px 0px 0px;"><textarea name="col_4" style="width:100px; text-align:center; padding:5px; height: 15px;"></textarea></th>';
			addRow += '<th style="padding:0px 0px 0px 0px;"><textarea name="col_5" style="width:100px; text-align:center; padding:5px; height: 15px;"></textarea></th>';
			addRow += '<th style="padding:0px 0px 0px 0px;"><textarea name="col_6" style="width:100px; text-align:center; padding:5px; height: 15px;"></textarea></th>';
	
			addRow += '<th style="padding:0px 0px 0px 0px;"><input type="button" value="삭제" class="btn04 delRowData" /></th> ';
			addRow += '</tr>'
				$("#columnBody").append(addRow);
			}
	});

	// 데이터 추가시 지방관서에 따른 지청 select box 생성
	$(".cv_note").live('change', function (){
		var $this = $(this);
		var cv_note = $this.val();
		var idx = $(".cv_note").index(this);
		
		var $cv_value = $(".cv_value");
		var defualt_option = '<option value="">지방관서</option>'; 
		$cv_value.eq(idx).html("");
		
		
		if ( cv_note != '' ) {
			$.ajax({
		        method			 : 'GET',
	        	url			 	 : "/civilComplaintData/localCivilComplaintPopupSelectBox",
		        data : {
		        	"local_name" : cv_note
		            },
		        dataType  		 :'json',    
		        success:function(data){
			       					
	
					if(data != null){
	
		                
		                for(var i=0; i < data.length; i++){
		                	$cv_value.eq(idx).append("<option value='" + data[i].cv_value + "'>" + data[i].cv_name + "</option>");
		                }
		                
		                
					} else {
						$cv_value.eq(idx).html(defualt_option);
					}
		            
				},
				error:function(x,e){
					$cv_value.eq(idx).html(defualt_option);
				}                      
			}); 
			
		} else {
			$cv_value.eq(idx).html(defualt_option);
		}
	})	

	//리포트 파라미터 삭제클릭시 TR 삭제
	 // 삭제기능
	$(".delRowData").live("click", function(){
		$(this).parent().parent().remove();		
	}); 

});

function delRowAjax(record_id, row_no){

	var result = confirm("데이터를 삭제 하시겠습니까? 삭제 후에는 복구가 불가능 합니다.");
	
	
	if(result){
		$.ajax({
		    type: "get",
		    url: "localCivilComplaintPopupDelete",
		    data: {
		    	record_id	: record_id,
		    	row_no		: row_no	
	    	},
		    dataType: "json",
		    success:function(result) {
		    	alert(result);
			} 
		});		
	}	
}
}    
```

