# javascript) 돔 선택 문제 해결(like eventBus)





```javascript
$(function(){
    buildSomething();
});


function buildSomething() {
			
    var html = "";

    for ( var i = 0; i < data.list1.length; i++ ) {

        html += '<div>';
        html += '	<div class="panel-toolbar">';
        html += '		<button type="button" class="btn_add">추가</button>';
        html += '	</div>';

        html += '	<div>';

        if ( data.list2 ) {

            for ( var j = 0; j < data.list2.length; j++ ) {

                if ( data.list1[i].idx1 == data.list2[j].idx1 ) {

                    html += '<div class="custom-control custom-checkbox" style="margin-bottom:7px;">';

                    html += '	<span>' + data.list2[j].nm + '</span>';
                    html += '</div>';

                }
            }

        }

        html += '	</div>';
        html += '</div>';

    }

    $("#js-page-content").empty();
    $("#js-page-content").append(html);
			
		
		
	eventBus();
		
	}
	
	
	
function eventBus() {

    // 추가 버튼 클릭이벤트 추가
    $(".btn_add").click(function() {
        add($(this));
    });

    // .. buildSometiong 안에 관련된 이벤트 리스너들 추가

}
```

