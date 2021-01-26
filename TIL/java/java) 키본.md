# java) 키본..

```java
    //List aList = new ArrayList();


        /*for ( int i = 0; i < aList.size(); i++ ) {
            List tmp = (List) aList.get(i);
            tmp.add(i);
        }*/

        List[] bList = new ArrayList[2];

        for ( int i = 0; i < bList.length; i++ ) {
            List tmp = new ArrayList();
            tmp.add(i+1);
            bList[i] = tmp;
        }

        System.out.println(bList[0]);
        System.out.println(bList[1]);
```

