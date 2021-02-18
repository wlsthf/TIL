# javascript) 돔 선택 문제 해결(like eventBus)





```javascript
// 최초 페이지 로드시 실행되는 함수
$(function(){
    buildSomething();
    
    init();
});



// 이벤트 리스너 등록
function init() {
    $("#btn").click(function() {
    	handleBtnClick();
	});
}



// 새롭게 추가된 돔에 대한 이벤트 리스너 등록
function eventBusSomeThing() {
    // 추가 버튼 클릭이벤트 추가
    $(".btn_add").click(function() {
        add($(this));
    });

    // .. buildSometiong 안에 관련된 이벤트 리스너들 추가

}



function handleBtnClick() {
    console.log('버튼을 클릭했어요!');
}



function buildSomething() {
	// 데이터를 받아온다고 가정
    var data = getData();
    var html = "";

    if ( data.list1 ) {
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
    }    

    $("#js-page-content").empty();
    $("#js-page-content").append(html);
		
	eventBusSomeThing();
		
}

```

