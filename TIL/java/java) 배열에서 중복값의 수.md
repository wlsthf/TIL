# java) 배열에서 중복값의 수



```java

	String[] arr= {"aaa","aaa","bbb","ccc","ddd","ccc","eee"};
		
	Map<String, Integer> map = new HashMap<String, Integer>();
	for(String key : arr) {
		map.put(key, map.getOrDefault(key, 0)+1);
	}
	System.out.println(map);

{aaa=2, ccc=2, bbb=1, eee=1, ddd=1}
```

