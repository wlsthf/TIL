# checkbox 값 받아서 처리하기

```html
<label><input type="checkbox" name="name" value="apple">김사과</label>
<label><input type="chekcbox" name="name" value="banana">반하나</label>
<labe><input type="checkbox" name="name" value="melon">한메론</labe>
```



#### java에서 처리

```java
String[] name = request.getParameterValues("name");

for ( int i = 0; i < name.lenght - 1; i++ ) {
    out.print(name[i] + ",");
}
out.print(name[name.length-1]);
```

