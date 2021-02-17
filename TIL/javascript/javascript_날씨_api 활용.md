# javascript ) 날씨 api 활용



[Open weather ](https://openweathermap.org/)



```javascript
<script src="https://code.jquery.com/jquery-3.3.1.min.js"/>
<script>
    // 도시이름
    var city = "seoul";

    // 날씨 api호출 ( 분당 60회 호출 가능 )
    var apiURI = "http://api.openweathermap.org/data/2.5/weather?q="+city+"&appid="+"api key를 입력";
    $.ajax({
        url      : apiURI,
        dataType : "json",
        method   : "GET",
        async    : "false",
        success  : function(data) {
            console.log(data);
            console.log("현재온도 : "+ (data.main.temp- 273.15) );
            console.log("현재습도 : "+ data.main.humidity);
            console.log("날씨 : "+ data.weather[0].main );
            console.log("상세날씨설명 : "+ data.weather[0].description );
            console.log("날씨 이미지 : "+ data.weather[0].icon );
            console.log("바람   : "+ data.wind.speed );
            console.log("나라   : "+ data.sys.country );
            console.log("도시이름  : "+ data.name );
            console.log("구름  : "+ (data.clouds.all) +"%" );
            var imgURL = "http://openweathermap.org/img/w/" + data.weather[0].icon + ".png";
            $("#img").attr("src", imgURL);
        }
    });
</script>
```



#### html

```html
<P> 서울의 날씨 : <img id="img" /> </P>
```

