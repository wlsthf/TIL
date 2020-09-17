# java) 자료형 가지고 놀기!



1단계 map

```java
// 넣기
Map<String, String> map = new HashMap<>();

String value = "값입니다.";

map.put("value", value);

// 꺼내기
System.out.println(map.get("value").toString());
```



2 단계 mapList

```java
// 넣기
Map(String, List<String>) mapList = new HashMap<>();
List<String> list = new ArrayList<>();

String value1 = "값1";
String value2 = "값2";

list.add(value1);
list.add(value2);

mapList.put("list", list);

// 꺼내기
List<String> tmpList = (List) mapList.get("list");

if ( tmpList != null && tmpList.size() > 0 ) {
    for ( int i = 0; i < tmpList.legnth; i++ ) {
        
		System.out.println(tmpList[i].toString());

    }
}
```



3단계 mapListMap

```java
// 넣기
Map(String, List<Map<String, String>) mapListMap = new HashMap<>();
List<Map<String, String> listMap = new ArrayList<>();

    
String[] valueArr = { "값1", "값2" }    

for ( int i = 0; i < 2; i++ ) {
    Map<String, String> tmpMap = new HashMap<>()
    tmpMap.put("value",valueArr[i]);    
    
    listMap.add(tmpMap);
} 


mapListMap.put("listMap", listMap);


// 꺼내기
Map(String, List<Map<String, String>) tmpMapListMap = new HashMap<>();
List<Map<String, String> tmpListMap = (List) tmpMapListMap.get("listMap");

if ( tmpList != null && tmpListMap.size() > 0 ) {
    for ( int i = 0; i < tmpListMap.legnth; i++ ) {
        Map<String, String> tmpMap = (Map) tmpListMap.get(i);
        
		System.out.println(tmpMap.get("value").toString());

    }
}
```





4단계 listList

..