# HTML) form enctype 속성

###### form 에서 method 가 POST 인 경우에만 사용가능



```html
<form method="POST" enctype"속성값"
```





| 속성값                            | 설명                                                         |
| --------------------------------- | ------------------------------------------------------------ |
| application/x-www-form-urlencoded | 기본값으로, 모든 문자들은 서버로 보내기 전에 인코딩됨을 명시 |
| multipart/form-data               | 모든 문자를 인코딩하지 않음을 명시함.이 방식은 form 요소가 파일이나 이미지를 서버로 전송할 때 주로 사용 |
| text/plain                        | 공백 문자(space)는 "+" 기호로 변환하지만, 나머지 문자는 모두 인코딩되지 않음을 명시 |





##### multipart/form-data에서 Controller method 예시

```java
@RequestMapping(value="/유아렐" , method=RequestMethod.POST)
public void 깐츄롤러의 어떤 메소드 (Model model, MultipartHttpServletRequest request, @RequestParam Map<String, Object> parameter) throws Exception {
    
    // request 객체로부터 배열을 받는다.
	String[] 같은이름_배열 = request.getParameterValues("같은이름");
	List<MultipartFile> 파일_리스트 = request.getFiles("파일"); 
    
    // map을 담을 리스트 생성
    List 같은이름_리스트 = new ArrayList();
    
	// null검사 해주고,
    if ( 같은이름_배열 != null && 같은이름_배열.length > 0 ) {
        for ( int i = 0; i < 같은이름_배열.length; i++ ) {
            // list에 담을 row 생성
        	Map row = new HashMap();
            
            // 값이 있는 것만 넣는다.
            // 파일은 파일편에서 자세하게 다룬다.
            if ( 같은이름_배열[i] != null && !같은이름_배열[i].equals("") ) {
                row.put("같은이름", 같은이름_배열[i]);
                
                // row를 list에 담는다
                같은이름_리스트.add(row);
            }      
        }        
    }
    
    parameter.put("같은이름_리스트", 같은이름_리스트);
       
    // 파라미터를 서비스로 보내고 결과를 받아 webFlow처리 해준다.
}
```

