# javascript ) checkbox 전체선택, 선택해제



### 쉬움이 버전

```javascript
$(function() {
    $(":checkbox:first").click(function() {
        controllAll($(this));
    })
});

function controllAll($this) {
    if( $this.is(":checked") ) {

        $(":checkbox").each(function() {
            $(this).prop("checked", true);
        });

    } else {
        
        $(":checkbox").each(function() {
            $(this).prop("checked", false);
        })
        
    }
}
```





### javascript

```javascript
$(document).ready(function(){
    var tbl = $("#checkboxTestTbl");

    // 테이블 헤더에 있는 checkbox 클릭시
    $(":checkbox:first", tbl).click(function(){
        // 클릭한 체크박스가 체크상태인지 체크해제상태인지 판단
        if( $(this).is(":checked") ){
            $(":checkbox", tbl).prop("checked", true);
        } else{
            $(":checkbox", tbl).prop("checked", false);
        }

        // 모든 체크박스에 change 이벤트 발생시키기               
        $(":checkbox", tbl).trigger("change");
    });

    // 헤더에 있는 체크박스외 다른 체크박스 클릭시
    $(":checkbox:not(:first)", tbl).click(function(){
        var allCnt = $(":checkbox:not(:first)", tbl).length;
        var checkedCnt = $(":checkbox:not(:first)", tbl).filter(":checked").length;

        // 전체 체크박스 갯수와 현재 체크된 체크박스 갯수를 비교해서 헤더에 있는 체크박스 체크할지 말지 판단
        if( allCnt==checkedCnt ){
            $(":checkbox", tbl).prop("checked", true);
        } else{
            $(":checkbox", tbl).prop("checked", false);
        }
    }).change(function(){
        if( $(this).is(":checked") ){
            // 체크박스의 부모 > 부모 니까 tr 이 되고 tr 에 selected 라는 class 를 추가한다.
            $(this).parent().parent().addClass("selected");
        } else{
            $(this).parent().parent().removeClass("selected");
        }
    });
});
```





#### html

```html
<table id="checkboxTestTbl" border="1px">
        <caption>체크박스 전체선택 테스트</caption>
        <colgroup>
            <col width="40px;"/>
            <col width="200px;"/>
            <col width="100px;"/>
        </colgroup>
        <tr>
            <th><input type="checkbox"/></th>
            <th>제목</th>
            <th>날짜</th>
        </tr>
        <tr>
            <td><input type="checkbox" /></td>
            <td>제목1</td>
            <td>날짜1</td>
        </tr>
        <tr>
            <td><input type="checkbox" /></td>
            <td>제목2</td>
            <td>날짜2</td>
        </tr>
        <tr>
            <td><input type="checkbox" /></td>
            <td>제목3</td>
            <td>날짜3</td>
        </tr>
        <tr>
            <td><input type="checkbox" /></td>
            <td>제목4</td>
            <td>날짜4</td>
        </tr>
        <tr>
            <td><input type="checkbox" /></td>
            <td>제목5</td>
            <td>날짜5</td>
        </tr>
        <tr>
            <td><input type="checkbox" /></td>
            <td>제목6</td>
            <td>날짜6</td>
        </tr>
    </table>
```





참고:  [스토브 훌로구](https://stove99.tistory.com/98?category=360125)