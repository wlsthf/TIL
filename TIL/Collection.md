# Collection

###  Collection

######   Arraylist처럼 여러 항목들을 나열한 데이터형을 다루는 유요한 클래스중 하나가 컬렉션

######  컬렉션 클래스는 여러가지 유용한 알고리즘을 구현한 메소드를 제공

######  컬렉션은 어레이리스트와 마찬가지로 java.util 패키지에 속해있고 import해야함

######  Collections 클래스의 메소드는 모두 static메소드의 형태로 제공되기 때문에 클래스명.메소드()로 사용

####  

#### 정렬 sort()

######  sort()메소드는 배열등의 데이터를 객체에 따라 순서대로 나열.

######  Integer의 경우 숫자의 순서대로 나열

######  String의 경우 알파벳 순서대로 나열

```java
 Collection.sort(배열명);
```

 

#### 역정렬 reverseOrder()

```java
 Collection.sort(배열명, Collections.reverseOrder());
```



#### 섞기 Shuffling()

```java
 Collection.shuffle(배열명);
```

