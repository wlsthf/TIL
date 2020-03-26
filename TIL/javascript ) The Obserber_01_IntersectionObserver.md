# javascript ) The Obserber_01_IntersectionObserver 

## IntersectionObserver 

###### 루트 영역(뷰포트와 대상 객체의 겹침을 감시)

###### 



## idex.html

```html
<!DOCTYPE html>
<html>
  <head>
    <title>test</title>
    <meta charset="UTF-8" />
  </head>

  <body>
    <div id="app"></div>
    <div class="box">
      <a class="item" href="#"></a>
      <a class="item" href="#"></a>
      <a class="item" href="#"></a>
    </div>

    <script src="src/index.js"></script>
  </body>
</html>
```



## style.css

```css
body {
  font-family: sans-serif;
}

.box {
  margin: 100vh 0;
  width: 200px;
  height: 300px;
}

.item {
  display: block;
  width: 200px;
  height: 300px;
  background-color: aqua;
}
```



## index.js

```javascript
import "./styles.css";

document.getElementById("app").innerHTML = `
<h1>Lazy Kitten!</h1>
<div>
  <p>스크롤이 고양이 이미지 위치까지 내려갔을 때 이미지를 동적 로딩합니다.</p>
  <p>스크롤을 내리시면 고양이를 볼 수 있습니다.</p>
  <p>콘솔을 확인해서 이미지가 로딩되었는지 체크하세요!</p>
</div>
`;

const io = new IntersectionObserver((entries, observer) => {
  entries.forEach(entry => {
    if (!entry.isIntersecting) {
      return;
    }
    const { target } = entry;
    target.style.backgroundImage = "url(https://placekitten.com/200/300)";
    console.log(`Load Success! ${target.style.backgroundImage}`);
    observer.unobserve(target);
  });
});

Array.from(document.querySelectorAll(".box a")).forEach(box => {
  io.observe(box);
});

```



## package.json

```json
{
  "name": "intersection",
  "version": "1.0.0",
  "description": "",
  "main": "index.html",
  "scripts": {
    "start": "parcel index.html --open",
    "build": "parcel build index.html"
  },
  "dependencies": {},
  "devDependencies": {
    "@babel/core": "7.2.0",
    "parcel-bundler": "^1.6.1"
  },
  "keywords": []
}
```







출처 : [huskyhoochu.com](https://www.huskyhoochu.com/js-observers/)