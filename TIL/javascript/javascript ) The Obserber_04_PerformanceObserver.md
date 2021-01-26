# javascript ) The Obserber_04_PerformanceObserver

## PerformanceObserver

###### 프로세스 성능 모니터링

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
	<p>
		<span>1부터 11355까지 합계: </span>
		<span id="answer"></span>
	</p>
	<script src="src/index.js">
</script>
</body>

</html>
```



## style.css

```css
body {
  font-family: sans-serif;
}
```



## index.js

```javascript
import Perfume from "perfume.js";
import "./styles.css";

document.getElementById("app").innerHTML = `
<h1>퍼포먼스 측정</h1>
<div>
  <p>PerformanceObserver는 최신 브라우저에만 쓸 수 있는 제한적인 옵저버입니다. 대안으로 쓸 수 있는 것들을 소개합니다.</p>
  <p>1. console.time & console.timeEnd</p>
  <a href="https://developer.mozilla.org/ko/docs/Web/API/Console/time" arget="_blank">console.time | MDN</a>
  <p>2. Perfume.js</p>
  <a href="https://github.com/Zizzamia/perfume.js" target="_blank">Zizzamia/perfume.js | GitHub</a>
</div>
`;

const perfume = new Perfume({
  firstPaint: true
});

function totalSum(num) {
  if (num <= 1) {
    return num;
  }

  return num + totalSum(num - 1);
}

// console.time
console.time();
document.getElementById("answer").innerHTML = totalSum(11355);
console.timeEnd();

// Perfume.js
perfume.start("totalSum");
totalSum(11355);
perfume.end("totalSum");

```



## package.json

```json
{
  "name": "performance",
  "version": "1.0.0",
  "description": "",
  "main": "index.html",
  "scripts": {
    "start": "parcel index.html --open",
    "build": "parcel build index.html"
  },
  "dependencies": {
    "perfume.js": "2.1.2"
  },
  "devDependencies": {
    "@babel/core": "7.2.0",
    "parcel-bundler": "^1.6.1"
  },
  "keywords": []
}
```







출처 : [huskyhoochu.com](https://www.huskyhoochu.com/js-observers/)