# javascript ) tr row 선택 데이터 뽑기

```javascript
$(window).load(function () {
 
        //시작
           S_Row();
            
     });
 
    //선택데이터
    function S_Row() {
        $("#a_chk").unbind('click');
        $("#a_chk").click(function () {
            var allbox = $(this).attr("checked");
            if (allbox == true) {
                $('table#table_name tr td input:checkbox').each(function () {
                    $(this).attr("checked", "checked");
                });
            } else {
                $('table#table_name tr td input:checkbox').each(function () {
                    $(this).attr("checked", "");
                });
            }
        });
 
    // tr 로우 
    var rows = $("table#table_name tr");
    
    // 로우 
    if (rows && rows.length > 0) {
        $(rows).each(function (idx) {
            if (idx > 0) {
 
                var startIdx = 1;
                var endIdx = rows[idx].childNodes.length;
                //시작점과 끝점을 for 문으로 돌려서 선택된 row
                for (i = startIdx; i <= endIdx; i++) {
                    //$(rows[idx].childNodes[i]).click(function () {
                    $(rows[idx]).find('td').eq(i).unbind('click');
                    $(rows[idx]).find('td').eq(i).click(function () {
                        
                        // 선택된 로우의 값 호출
                        var ID = $(rows[idx]).find('td').eq(0).children('input[type="checkbox"]').val();          //GUID
                        alert("checkbox value : " + ID);
                        //ID 값을 넘겨서 ViewPage를 호출한다.
                    });
                }
 
                //마우스오버 시에 색표현
                $(this).mouseover(function () {
                    
                    //$(rows[idx]).addClass('mouseovercolor').attr('style', 'cursor:pointer;cursor: hand;'); class로 주려면
                    //로우색 변환 color 변경 
                    $(rows[idx]).attr('style', 'cursor:pointer; cursor: hand;background-color:#f8f8f8;');
 
                });
                    
                //마우스 아웃
                $(this).mouseout(function () {
                    //로우색 복귀
                    $(rows[idx]).css('background-color', '').attr('style', '');
                });
            }
 
 
        });
        }
}
 
}
```



출처 : [빛나는 리오a 티스토리](https://rios.tistory.com/entry/JS-tr-%EB%A1%9C%EC%9A%B0-%EC%84%A0%ED%83%9D-%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%BD%91%EA%B8%B0?category=711004)