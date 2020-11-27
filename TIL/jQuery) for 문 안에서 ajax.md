# jQuery) for 문 안에서 ajax



```javascript
for ( var i = 0; i < obj.nm_arr.length; i++ ) {
    let pararam = {};

    param.layerNm = obj.nm_arr[i];
    param.param = obj.param_arr[i];

	(function(i){
		$.ajax({
			url		: "/지오서버",
			dataType : 'application/json',
			type     : "GET",
			data     : param,
			async    : false,
			success  : function(layer) {
				map.addLayer(layer);
			},
             error    : function(e) {
				console.log(e);
			}
		}); 
	})(i);
}
```

