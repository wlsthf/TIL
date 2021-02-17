# javascript ) The Obserber_03_MutationObserver

## MutationObserver

###### 객체의 속성 변경을 감시

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
	<div class="box">
		<p>Click me</p>
	</div>

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

.box {
  width: 300px;
  height: 300px;
  background-color: #000;
  display: flex;
  align-items: center;
  justify-content: center;
}

.box p {
  color: white;
  font-size: 20px;
  font-weight: bold;
}
```



## index.js

```javascript
import "./styles.css";

document.getElementById("app").innerHTML = `
<h1>Mutation Observer</h1>
<div>
  <p>박스가 사라질 때까지 계속 클릭하세요!</p>
</div>
`;

let count = 0;
const mo = new MutationObserver(entries => {
  entries.forEach(entry => {
    const { target } = entry;
    target.parentElement.style.backgroundColor = target.innerHTML;
  });
});

const box = document.querySelector(".box");
box.addEventListener(
  "click",
  function() {
    box.children[0].innerHTML = `rgb(${count * 2}, ${count * 3}, ${count * 4})`;
    count++;
  },
  false
);

mo.observe(box.children[0], {
  attributes: true,
  childList: true,
  characterData: true
});
```



## package.json

```json
{
  "name": "mutation",
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