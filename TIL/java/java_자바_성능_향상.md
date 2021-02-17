# java) 자바 성능 향상



## String 보다는 StringBuffer

```java
String str = "aaa";
str = str + "bbb";
str += "ccc";
// 연산을 할 때마다 객체를 생성하고 이전 객체는 garbage collection된다.

StringBuffer sb = new StringBuffer();
sb.append("aaa");
sb.append("bbb");
```



## 더 빠른 연산자

```java
// 증감연산자가 가장 빠르다.
int i = 0;
i++;

// += 가 더 빠르다
int a = 0;
a = a + 1;
a += 1;

// 곱셈 나눈셈 보다는 shift연산이 빠르다.
int b = 2;
b >> 2; // b == 1
```



## 마구잡이로 객체를 만들지 않는다.

```java
for ( int i = 0; i < xxx.size(); i++ ) {
	String str = xxx.get(i).toString();
}

for ( String str : xxx ) {
    // 이렇게 사용하거나
}

String str;
for ( int i = 0; i < xxx.size(); i++ ) {
    str = xxx.get(i).toString();
    // 이렇게 사용하자
}
```



## 변수 범위와 타입 

- ###### 지역 메소드 변수가 스택영역에 저장 되므로 가장빠르다.

- ###### int 가 가장 빠른데 구지이이이 long 을 쓸필요 없다.



## 메소드 호출

- ###### 자주 쓰는 메소드는 static으로 선언

- ###### 자주 참조하는 변수는 final 사용 ( 배열 등도 마찬가지 )



## 배열 길이 체크할때 try- catch 사용



## 적절한 버퍼 사용

`BufferedInputStream,BufferedOutputStream`





참조 : 충남대학교 컴퓨터과학과 김영국(ykim@cs.chungnam.ac.kr)

