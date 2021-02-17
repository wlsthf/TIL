# java ) 시간 관련

```java
public String nvlDate(Map map, String key) {
    return nvlDate(map, key, "-");
}

public String nvlDate(Map map, String key, String delimeter) {
    String val = nvl(map, key);
    if ( val.isEmpty() || val.length()  < 8 ) return val;

    if ( val.substring(4, 6).equals("00") ) {

        return val.substring(0, 4);

    } else if ( val.substring(6, 8).equals("00") ) {

        return val.substring(0, 4) + delimeter + val.substring(4, 6);
    }

    return val.substring(0, 4) + delimeter + val.substring(4, 6) +delimeter + val.substring(6, 8);
}

public String nvlDateKr ( Map map, String key ) {
    String val = nvl(map, key);
    if ( val.isEmpty() || val.length()  < 8 ) return val;

    if ( val.substring(4, 6).equals("00") ) {

        return val.substring(0, 4) + " 년";

    } else if ( val.substring(6, 8).equals("00") ) {

        return val.substring(0, 4) + " 년 " + val.substring(4, 6) + " 월";
    }

    return val.substring(0, 4) + " 년 " + val.substring(4, 6) + " 월 " + val.substring(6, 8) + " 일";
}

public String nvlTime(String time) {

    String val =time;

    if ( val.isEmpty() || val.length() < 6 ) return val;
    return val.substring(0, 2) + ":" + val.substring(2, 4) + ":" + val.substring(4, 6);
}
```

