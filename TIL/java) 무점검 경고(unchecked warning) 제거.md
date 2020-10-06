# java) 무점검 경고(unchecked warning) 제거



**@SuppressWarnings(“unchecked”) 으로 제거가능..**



###### 프로그래밍을 할 때 경고는 무시하고 코딩을 하는 경우가 있는데 진짜 중요한 경고를 판별하기위해서 모든 경고도 제거하고 코딩하는 것이 바람직하다.

###### 아래와같이 경고를 제거하고 주석을 달아주자

```java
// 인자로 전달된 T의 자료형이 확실하다.
@SuppressWarnings(“unchecked”) T something = (T) list.get(0);
```



