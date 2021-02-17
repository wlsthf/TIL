# java) 반올림 2가지

## Math.round()

```java
double pie = 3.14159265358979;
System.out.println(Math.round(pie)); //결과 : 3
System.out.println(Math.round(pie*100)/100.0); //결과 : 3.14
System.out.println(Math.round(pie*1000)/1000.0); //결과 : 3.142
```



## String.format()

```java
double pie = 3.14159265358979;
double money = 4424.243423;
System.out.println(String.format("%.2f", pie)); //결과 : 3.14
System.out.println(String.format("%.3f", pie)); //결과 : 3.142
System.out.println(String.format("%,.3f", money)); //결과 : 4,424.243
```



## Math.round 와 String.format()의 다른점

```java
double money = 5000.000;
System.out.println(Math.round(money*1000)/1000); //결과 5000
System.out.println(String.format("%.3f", money)); //결과 : 5000.000
```

