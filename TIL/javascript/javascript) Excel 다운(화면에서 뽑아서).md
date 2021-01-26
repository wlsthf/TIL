# Excel 다운(화면에서 뽑아서)

```javascript
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
```

