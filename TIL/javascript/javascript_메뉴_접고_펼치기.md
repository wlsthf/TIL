# javacsript ) 메뉴 접고 펼치기



### HTML

```javascript
<div>
    <ul>
        <li class="menu">
            <a><img src="" alt="상위메뉴이미지1"/></a>
            <ul class="hide">
                <li>메뉴1-1</li>
                <li>메뉴1-2</li>
                <li>메뉴1-3</li>
                <li>메뉴1-4</li>
                <li>메뉴1-5</li>
                <li>메뉴1-6</li>
            </ul>
        </li>
 
        <li class="menu">
            <a><img src="" alt="상위메뉴이미지2"/></a>
            <ul class="hide">
                <li>메뉴2-1</li>
                <li>메뉴2-2</li>
                <li>메뉴2-3</li>
                <li>메뉴2-4</li>
                <li>메뉴2-5</li>
                <li>메뉴2-6</li>
            </ul>
        </li>
    </ul>
</div>
```





### CSS

```css
    .menu a{cursor:pointer;}
    .menu .hide{display:none;}
```





### script

```javascript
// html dom 이 다 로딩된 후 실행된다.
    $(document).ready(function(){
        // memu 클래스 바로 하위에 있는 a 태그를 클릭했을때
        $(".menu>a").click(function(){
            // 현재 클릭한 태그가 a 이기 때문에
            // a 옆의 태그중 ul 태그에 hide 클래스 태그를 넣던지 빼던지 한다.
            $(this).next("ul").toggleClass("hide");
        });
    });
```





### script - sliding

```javascript
  // html dom 이 다 로딩된 후 실행된다.
    $(document).ready(function(){
        // menu 클래스 바로 하위에 있는 a 태그를 클릭했을때
        $(".menu>a").click(function(){
            var submenu = $(this).next("ul");
 
            // submenu 가 화면상에 보일때는 위로 보드랍게 접고 아니면 아래로 보드랍게 펼치기
            if( submenu.is(":visible") ){
                submenu.slideUp();
            }else{
                submenu.slideDown();
            }
        });
    });
```





### script   + mouseover 

```javascript
    $(document).ready(function(){
        $(".menu>a").click(function(){
            var submenu = $(this).next("ul");
 
            // submenu 가 화면상에 보일때는 위로 보드랍게 접고 아니면 아래로 보드랍게 펼치기
            if( submenu.is(":visible") ){
                submenu.slideUp();
            }else{
                submenu.slideDown();
            }
        }).mouseover(function(){
            $(this).next("ul").slideDown();
        });
    });
```





### script

```javascript
 $(document).ready(function(){
        $(".menu>a").click(function(){
            var submenu = $(this).next("ul");
 
            // submenu 가 화면상에 보일때는 위로 보드랍게 접고 아니면 아래로 보드랍게 펼치기
            if( submenu.is(":visible") ){
                submenu.slideUp();
            }else{
                submenu.slideDown();
            }
        }).mouseover(function(){
            $(this).next("ul").slideDown();
        });
 
 
        // menu class 중에 두번째 있는 menu 의 하위에 있는 a태그에 클릭 이벤트를 발생시킨다.
        $(".menu:eq(1)>a").click();
    });
```



출처: [스토브 훌로구]( https://stove99.tistory.com/103?category=360125)