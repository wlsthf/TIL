# CSS) scroll - table에서 활용





```html
<div style="width: 1000px; heigth: 500px; overflow: auto">
    <table style: width:100%; heigth:100%>
        <tr><td></td></tr>
    </table>
</div>
```



auto =  없었다가 생김

scroll = 처음부터 있음

hidden = 스크롤 표시 x





overflow = xy 둘다

overflow-x = x만

overflow-y = y만 







tboy만 스크롤 하고 싶을 때

```html
<div style="width: 1000px; heigth: 500px;">    
	<table style: width:100%; heigth:100%>
         <thead>
            <tr><th></th></tr>  
         </thead>
         <tbody style="display: block;width: 1000px; height: 500px; overflow: auto;">
             <tr><td></td></tr>  
         </tbody>
	</table>
</div>
```

display : block 추가