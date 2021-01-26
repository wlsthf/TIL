# Ajax사용을 위한 JsonView 설정

## 1. pom.xml

```xml
<dependency>        
    <groupId>net.sf.json-lib</groupId>        
    <artifactId>json-lib</artifactId>        
    <version>2.4</version>        
    <classifier>jdk15</classifier>    
</dependency>
 
<dependency> 
    <groupId>org.codehaus.jackson</groupId> 
    <artifactId>jackson-mapper-asl</artifactId> 
    <version>1.6.4</version> 
</dependency>
```



## 2. dispatcher-servlet.xml

```xml
<bean class="org.springframework.web.servlet.view.BeanNameViewResolver" id="viewResolver" p:order="0"/>
<bean class="org.springframework.web.servlet.view.json.MappingJacksonJsonView" id="jsonView">
    <property name="contentType" value="application/json;charset=UTF-8"/>
</bean>
```



## 3. web.xml

```xml
<servlet-mapping>
    <servlet-name>action</servlet-name>
    <url-pattern>*.do</url-pattern>
</servlet-mapping>
<servlet-mapping>
    <servlet-name>action</servlet-name>
    <url-pattern>*.ajax</url-pattern>
</servlet-mapping>
```



## 4. Controller.java

```java
@RequestMapping("/test.do")
public String test(@ModelAttribute("VO") CommentVO commentVO, ModelMap model) throws Exception {
    return "test/test";
}
 
@RequestMapping("/test.ajax")
public ModelAndView testAjax(@ModelAttribute("VO") CommentVO commentVO, ModelMap model) throws Exception {
 
    ModelAndView modelAndView = new ModelAndView("jsonView",resultMap);
    Map resultMap = new HashMap();
    resultMap.put("result1", "1");
    resultMap.put("result2", "2");
 
    return modelAndView;
}
```



## 5. test.jsp

```jsp
<script type="text/javascript">
 
$.post("${pageContext.request.contextPath}/test.ajax",
    {
        test1: "1111",
        test2: "2222"
    },
    function(data) {
        alert("result: " + data);
    }
);
 
</script>
```

