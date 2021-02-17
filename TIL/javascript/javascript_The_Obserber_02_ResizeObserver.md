# javascript ) The Obserber_02_ResizeObserver

## ResizeObserver

###### 객체의 너비, 높이의 변화를 감시

###### 



## idex.html

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Parcel Sandbox</title>
    <meta charset="UTF-8" />
  </head>

  <body>
    <div id="app"></div>
    <div class="box"></div>
    <script src="src/index.js"></script>
  </body>
</html>
```



## style.css

```css
body {
  font-family: sans-serif;
  margin: 0;
}

.box {
  background-color: aqua;
  width: 100vw;
  height: 70px;
}
```



## index.js

```javascript
import ResizeObserver from "resize-observer-polyfill";
import "./styles.css";

document.getElementById("app").innerHTML = `
<h1>Resize Observer</h1>
<div>
  <p>창을 늘였다 줄였다 하면서 너비를 관찰해 보세요!</p>
</div>
`;

const ro = new ResizeObserver(entries => {
  entries.forEach(entry => {
    const { target } = entry;
    target.innerHTML = `현재 너비: ${target.clientWidth} px`;
  });
});

Array.from(document.querySelectorAll(".box")).forEach(box => {
  ro.observe(box);
});
```



## package.json

```json
{
  "name": "resizeobserver",
  "version": "1.0.0",
  "description": "",
  "main": "index.html",
  "scripts": {
    "start": "parcel index.html --open",
    "build": "parcel build index.html"
  },
  "dependencies": {
    "resize-observer-polyfill": "1.5.1"
  },
  "devDependencies": {
    "@babel/core": "7.2.0",
    "parcel-bundler": "^1.6.1"
  },
  "keywords": []
}
```







출처 : [huskyhoochu.com](https://www.huskyhoochu.com/js-observers/)