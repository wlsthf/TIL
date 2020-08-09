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
public void WriteCsv() {     
	//출력 스트림 생성
    BufferedWriter bufWriter = null;
    try {
        bufWriter = Files.newBufferedWriter(Paths.get("주소"),Charset.forName("UTF-8"));

        //csv파일 읽기
        List<List<String>> allData = readCSV();

        for(List<String> newLine : allData){
        	List<String> list = newLine;
        	for(String data : list){
        		bufWriter.write(data);
        		bufWriter.write(",");
        	}
        	//추가하기
        	bufWriter.write("새로운 값");
        	//개행코드추가
        	bufWriter.newLine();
        }
    } catch(FileNotFoundException e) {
    	e.printStackTrace();
    } catch(IOException e) {
    	e.printStackTrace();
    } finally {
    	try {
    		if ( bufWriter != null ) {
    			bufWriter.close();
    		}
    	} catch(IOException e) {
    		e.printStackTrace();
    	}
    }
}
```





참조:[정아마추어 코딩 블로그](https://jeong-pro.tistory.com/70)