# XML 시작

## XML 이란?

- ###### XML은 HTML과 매우 비슷한 문자 기반의 마크업 언어(text-based markup language)

- ###### 사람과 기계가 동시에 읽기 편한 구조

- ###### XML은 HTML처럼 데이터를 보여주는 목적이 아닌, 데이터를 저장하고 전달할 목적

- ###### XML 태그는 HTML 태그처럼 미리 정의되어 있지 않고, 사용자가 직접 정의할 수 있다.



## XMl 특징

1. ###### XML은 다른 목적의 마크업 언어를 만드는 데 사용되는 다목적 마크업 언어

2. ###### XML은 다른 시스템끼리 다양한 종류의 데이터를 손쉽게 교환할 수 있도록 해준다.

3. ###### XML은 새로운 태그를 만들어 추가해도 계속해서 동작하므로, 확장성이 좋다.

4. ###### XML은 데이터를 보여주지 않고, 데이터를 전달하고 저장하는 것만을 목적으로 한다.

5. ###### XML은 텍스트 데이터 형식의 언어로 모든 XML 문서는 유니코드 문자로만 이루어진다.

6. ###### XML은 문서용 마크업 언어를 정의하기 위한 메타언어인 SGML(Standard Generalized Markup Language)을 기반으로 만들어짐



## XML 표준

######  1996년 W3C 시작, 2008년에는 XML 1.0의 다섯 번째 버전이 발표

[W3C ]([https://www.w3.org/TR/xml](https://www.w3.org/TR/xml/))



## XML 설계 목적

1. XML은 인터넷상에서 명확하게 사용할 수 있어야 한다.
2. XML은 다양한 응용 프로그램을 지원해야 한다.
3. XML은 SGML과 호환되어야 한다.
4. XML 문서를 처리하는 프로그램은 손쉽게 작성될 수 있어야 한다.
5. XML에서 제공하는 옵션의 수는 최소한으로 유지되어야 한다.
6. XML 문서는 인간이 읽을 수 있어야 하며, 의미가 명확해야 한다.
7. XML의 설계는 빠르게 이루어져야 한다.
8. XML의 설계는 공식적이면서 간결해야 한다.
9. XML 문서는 작성하기 쉬워야 한다.
10. XML 마크업의 간결성은 그다지 중요하지 않다.





## HTML로부터 데이터 분리



##### javascript 

```javascript
function loadDoc() {

    var xmlHttp = new XMLHttpRequest();

    xmlHttp.onreadystatechange = function() {

        if(this.status == 200 && this.readyState == this.DONE) {

            displayData(xmlHttp);

        }

    };

    xmlHttp.open("GET", "/examples/media/korean_major_cities.xml", true);

    xmlHttp.send();

}

 

function displayData(xmlHttp) {

    var xmlObj, cityList, result, idx;

    xmlObj = xmlHttp.responseXML; // 요청한 데이터를 XML DOM 객체로 반환함.

    result = "<table><tr><th>도시 이름</th><th>행정구역</th></tr>";

    cityList = xmlObj.getElementsByTagName("city");

    for(idx = 0; idx < cityList.length; idx++) {

        result += "<tr><td>" +

            cityList[idx].getElementsByTagName("name")[0].childNodes[0].nodeValue + "</td><td>" +

            cityList[idx].getElementsByTagName("class")[0].childNodes[0].nodeValue + "</td></tr>";

    }

    result += "</table>";

    document.getElementById("text").innerHTML = result;

}
```





##### korean_major_cities.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>

<korean_cities>
    <city>
        <name>서울</name>
        <class>특별시</class>
    </city>
    <city>
        <name>부산</name>
        <class>광역시</class>
    </city>
    <city>
        <name>인천</name>
        <class>광역시</class>
    </city>
    <city>
        <name>대전</name>
        <class>광역시</class>
    </city>
    <city>
        <name>광주</name>
        <class>광역시</class>
    </city>
    <city>
        <name>대구</name>
        <class>광역시</class>
    </city>
    <city>
        <name>울산</name>
        <class>광역시</class>
    </city>
    <city>
        <name>수원</name>
        <class>시</class>
    </city>
    <city>
        <name>청주</name>
        <class>시</class>
    </city>
    <city>
        <name>목포</name>
        <class>시</class>
    </city>
</korean_cities>
```

