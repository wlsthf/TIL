# java ) nvl 활용

#### nvl (Nuclear valosin-containing protein-like) : null 값 처리

```java
public String nvl(Map map, String key, String defaultValue) {

    String value = nvl(map, key);

    return value.isEmpty() ? defaultValue : value;

}

public String nvl(Map map, String key) {
    if ( map == null ) {
        return "";
    }

    Object obj = null;
    if ( map.containsKey(key) ) {
        obj = map.get(key);
    } else if ( map.containsKey(key.toUpperCase()) ) {
        obj = map.get(key.toUpperCase());
    } else {
        return "";
    }
    return obj == null ? "" : String.valueOf(obj);
}

public int nvlInt(Map map, String key, int defaultValue) {

    if ( map == null ) {
        return defaultValue;
    }

    Object obj = null;

    if ( map.containsKey(key) ) {
        obj = map.get(key);
    } else if (map.containsKey(key.toUpperCase())) {
        obj = map.get(key.toUpperCase());
    } else {
        return defaultValue;
    }

    return obj == null ? defaultValue : Integer.parseInt(String.valueOf(obj));

}

public int nvlInt(Map map, String key) {
    return nvlInt(map, key, 0);
}
```

