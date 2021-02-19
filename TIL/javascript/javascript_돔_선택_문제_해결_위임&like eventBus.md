# javascript) 돔 선택 문제 해결(like eventBus, 이벤트 위임)



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





## delegate 개념

```javascript
// jQuery 1.4.3+
$( elements ).delegate( selector, events, data, handler );
// jQuery 1.7+
$( elements ).on( events, selector, data, handler );

$( "#foo" ).on( "click", function() {
  alert( $( this ).text() );
});
$( "#foo" ).trigger( "click" );
```



### 예시

```html
<ul id="menu">
  <li><button id="file">파일</button></li>
  <li><button id="edit">편집</button></li>
  <li><button id="view">보기</button></li>
</ul>
```



Javascript

```javascript
document.getElementById("menu").addEventListener("click", function(e) {
  var target = e.target;
  if (target.id === "file") {
    // 파일 메뉴 동작
  } else if (target.id === "edit") {
    // 편집 메뉴 동작
  } else if (target.id === "view") {
    // 보기 메뉴 동작
  }
});
```





jQuery

```javascript
// 이벤트 위임1
$("#menu").on("click", "li button", function() {
  if (this.id === "file") {
    // 파일 메뉴 동작
  } else if (target.id === "edit") {
    // 편집 메뉴 동작
  } else if (target.id === "view") {
    // 보기 메뉴 동작
  }
});

// 이벤트 위임2
$("#menu").on("click", "#file", function() {
  // 파일 메뉴 동작
});
$("#menu").on("click", "#edit", function() {
  // 편집 메뉴 동작
});
$("#menu").on("click", "#view", function() {
  // 보기 메뉴 동작
});

// 이벤트 위임3
$("#menu li button").click(function() {
    
});
$("#menu").on("myCustomEvent", "#file", function() {
  // 파일 메뉴 동작
});
$("#menu").on("myCustomEvent", "#edit", function() {
  // 편집 메뉴 동작
});
$("#menu").on("myCustomEvent", "#view", function() {
  // 보기 메뉴 동작
});
```

