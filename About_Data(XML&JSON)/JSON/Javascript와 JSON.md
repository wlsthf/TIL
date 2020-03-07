# Javascript와 JSON



## JSON.stringify()

```javascript
JSON.stringify(value)
```

```javascript
var dog = {name: "식빵", family: "웰시코기", age: 1, weight: 2.14}; // 자바스크립트 객체

var data = JSON.stringify(dog);                    // 자바스크립트 객체를 문자열로 변환함.

document.getElementById("json").innerHTML = data;
```

###### 인수로 전달받은 자바스크립트 객체를 문자열로 변환하여 반환

###### value에 변환할 자바스크립트 객체를 전달하고 이메소드는 UTF-16으로 인코딩된 JSON 형식의 문자열을 반환한다.



## JSON.parse()

```javascript
JSON.parse(text)
```

```javascript
var data = '{"name": "식빵", "family": "웰시코기", "age": 1, "weight": 2.14}'; // JSON 형식의 문자열

var dog = JSON.parse(data);                       // JSON 형식의 문자열을 자바스크립트 객체로 변환함.

document.getElementById("json").innerHTML = dog + "<br>";
document.getElementById("json").innerHTML += dog.name + ", " + dog.family;
```

###### JSON.stringify() 메소드와는 반대로 인수로 전달받은 문자열을 자바스크립트 객체로 변환하여 반환

###### 해당 문자열은 반드시 유효한 JSON 형식의 문자열이어야 한다.

###### 만약 JSON 형식에 맞지 않는 문자열을 전달하면, 자바스크립트는 오류를 발생한다.



## toJSON()

```javascript
YYYY-MM-DDTHH:mm:ss.sssZ

또는

±YYYYYY-MM-DDTHH:mm:ss.sssZ
```

```javascript
var date = new Date();   // 자바스크립트 Date 객체
var str = date.toJSON(); // Date 객체를 JSON 형식의 문자열로 변환함.
 

document.getElementById("json").innerHTML = date + "<br>";
document.getElementById("json").innerHTML += str;
```

###### 자바스크립트의 Date 객체의 데이터를 JSON 형식의 문자열로 변환하여 반환한다.

###### 따라서 이 메소드는 Date.prototype 객체에서만 사용할 수 있다.

 

###### toJSON() 메소드는 접미사 Z로 식별되는 UTC 표준 시간대의 날짜를 ISO 8601 형식의 문자열로 반환한다.

###### 따라서 이 문자열은 언제나 24개나 27개의 문자로 이루어지며, 다음과 같은 형식을 따른다.