# java) csv파일 읽기, 쓰기



csv파일 읽기 => csv파일을 저장하고 파일을 불러와서 읽는다.

```java
public List ReadCsv(Map parameter) {
    String filePath = parameter.get("file_path");
    //반환용 리스트
    List<List<String>> ret = new ArrayList<List<String>>();
    BufferedReader br = null;

    try {
        br = Files.newBufferedReader(Paths.get(filePath));
        //Charset.forName("UTF-8");
        String line = "";

        while ( (line = br.readLine()) != null ) {
            //CSV 1행을 저장하는 리스트
            List<String> tmpList = new ArrayList<String>();
            String array[] = line.split(",");
            //배열에서 리스트 반환
            tmpList = Arrays.asList(array);
            System.out.println(tmpList);
            ret.add(tmpList);
        }
    } catch(FileNotFoundException e) {
        e.printStackTrace();
    } catch(IOException e) {
        e.printStackTrace();
    } finally {
        try {
            if ( br != null ) {
                br.close();
            }
        } catch(IOException e) {
            e.printStackTrace();
        }
    }
    
    return ret;

}
```



csv파일 쓰기

```java

```





참조:[정아마추어 코딩 블로그](https://jeong-pro.tistory.com/70)