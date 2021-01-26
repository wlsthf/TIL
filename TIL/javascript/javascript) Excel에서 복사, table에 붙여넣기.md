# Excel에서 복사, table에 붙여넣기

```javascript
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
		                if (column) $("#columnBody").find("tr:nth-child("+(i+1+rowoffset)+")").find("td:nth-child("+(j+1+coloffset)+")").find("textarea").val(column);
		            }
		        }	    	
		    }
		}, 10);
	});
```

