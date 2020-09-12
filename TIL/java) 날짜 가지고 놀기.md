# java) 날짜 가지고 놀기



```java
DateFormat df = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss", Locale.KOREA);
Date today = new Date();
String dete = df.format ( today );


Calendar cal = Calendar.getInstance();
 
//현재 년도, 월, 일
int year = cal.get ( cal.YEAR );
int month = cal.get ( cal.MONTH ) + 1 ;
int date = cal.get ( cal.DATE ) ;
 
 
//현재 (시,분,초)
int hour = cal.get ( cal.HOUR_OF_DAY ) ;
int min = cal.get ( cal.MINUTE );
int sec = cal.get ( cal.SECOND );

```

