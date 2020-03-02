# Spring Tiles

#### spring Tiles 란?

###### 뷰단의 header, footer 등을 page include 방식으로 나눠 기본구조를 쉽게 적용하기 위한 템플릿 프레임워크

#### 장점 

###### include 디자인을 변경하면 페이지를 전체적으로 수정해야 하는 번거로움을 없애고 일관적인 페이지 관리 가능



------



#### 적용 순서

1. pom.xml 에 tiles 관련 dependency 추가
2. servlet-context.xml 파일에 타일즈 View Resolver 추가
3. Tiles 관련 설정 xml 추가
4. 기본 레이아웃 jsp 추가



------



## 1. pom.xml dependecy 추가

```xml
<properties>
    <!-- ... -->
    <!-- ... -->
    <org.apache.tiles-version>3.0.5</opg.apache.tiles-version>
</properties>
<!-- Tiles -->
<dependency>
	<groupId>org.apache.tiles</groupId>
    <artufactId>tiles-servlet</artufactId>
    <version>{org.apache.tiles-version}</version>
</dependency>
<dependency>
	<groupId>org.apache.tiles</groupId>
    <artufactId>tiles-api</artufactId>
    <version>{org.apache.tiles-version}</version>
</dependency>
<dependency>
	<groupId>org.apache.tiles</groupId>
    <artufactId>tiles-jsp</artufactId>
    <version>{org.apache.tiles-version}</version>
</dependency>
<dependency>
	<groupId>org.apache.tiles</groupId>
    <artufactId>tiles-core</artufactId>
    <version>{org.apache.tiles-version}</version>
</dependency>
<dependency>
	<groupId>org.apache.tiles</groupId>
    <artufactId>tiles-template</artufactId>
    <version>{org.apache.tiles-version}</version>
</dependency>
```



## 2. servlet-context 파일에 Tiles View Resolver bean 추가

```xml
<bean id="tilesViewResolver" 
      class="org.springframework.web.servlet.view.UrlBaseViewResolver">
    <property name="viewClass"  
              value="org.springframework.web.servlet.view.tiles3.TilesView"/>
    <property name="order" value="1" /><!-- 순서를 우선으로 지정 -->
</bean>
<bean id="tilesConfigurer" 
      class="org.springframework.web.servlet.view.tiles3.TilesConfigurer">
    <property>
    	<list>
        	<value>/WEB-INF/tiles/tiles-def.xml</value>
        </list>
    </property>
</bean>

<!-- order 속성을 사용하는 다른 부분은 2번을 지정해야함 -->

<property name="order" value="2" />
```

###### order 속성을 사용하는 다른곳은 설정값을 다르게 주어야함

###### order 속성 1로 지정 -> tiles를 우선적으로 로드 시킨다.



## 3. /WEB-INF/tiles/tiles-def.xml 설정

###### Tiles layout을 적용 하는 화면과 적용하지 않는 화면을 구분하는 설정

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOTYPE tiles-definitions PUBLIC
	"-//Apache Software Foundation//DTD Tiles Configuraion 3.0//EN"
	"http://tiles.apache.org/dtds/tiles-config_3_0.dtd">

<tiles-definitions>

	<!-- (1)레이아웃을 적용하지 않는 화면 -->
	<definition name=".login" template="/WEB-INF/jsp/tileLayout/loginLayout.jsp">
        <put-attribute name="title" > 제목입력 </put-attribute>
        <put-attribute name="header" value="/WEB-INF/jsp/tilesView/header.jsp" />
        <put-attribute name="menu" value="" />        
        <put-attribute name="footer" value="" />
    </definition>
 
    <!-- (2) 레이아웃을 적용하는화면-->
    <definition name=".root" template="/WEB-INF/jsp/tileLayout/baseLayout.jsp">
        <put-attribute name="title"> 제목입력 </put-attribute>
        <put-attribute name="header" value="/WEB-INF/jsp/tilesView/header.jsp" />
        <put-attribute name="menu" value="/WEB-INF/jsp/tilesView/menu.jsp" />        
        <put-attribute name="footer" value="/WEB-INF/jsp/tilesView/footer.jsp" />
    </definition>
    
    <!-- 빈페이지 -->
	<definition name="*/*.empty" template="/WEB-INF/view/jsp/layouts/empty/layout.jsp">
		<put-attribute name="title"> 제목입력 </put-attribute>
		<put-attribute name="contents" value="/WEB-INF/view/jsp/{1}/{2}.jsp" />
	</definition>

	<!-- 시스템 관련 페이지 (ex. error/webflowTwist -->
	<definition name="*/*.system" template="/WEB-INF/view/jsp/layouts/system/layout.jsp">
		<put-attribute name="contents" value="/WEB-INF/view/jsp/system/{1}/{2}.jsp" />
	</definition>
    
    <!-- (1) -->    
    <definition name="/login/*" extends=".login">
      <put-attribute name="body" value="/WEB-INF/jsp/login/{1}.jsp" />
    </definition>
 
    <!-- (2) -->
    <definition name="/*/*" extends=".root">      
    	<put-attribute name="body" value="/WEB-INF/jsp/{1}/{2}.jsp" />
    </definition>
    
    <definition name="*/*" extends="default_layout">
		<put-attribute name="title"> 제목입력 </put-attribute>
		<put-attribute name="contents" value="/WEB-INF/viewjsp/{1}/{2}.jsp" />
	</definition>
    
</tiles-definitions>
```

###### (1) header 에는 디자인이없는 공통 라이브러리들이 참조 될것이고 로그인 페이지는 header만 참조

######  	경로는 구성에 맞게 설정, definition 의 template 속성이 **기본적으로 틀이 잡힐** 레이아웃 jsp이고  그곳에 put-attribute를 넣는 방식으로 설정

###### 	두번째 extends 쪽 definition 을 살펴보면 name 에 매핑을 걸고 해당매핑일때 참조될 jsp의 주소를 가리킴

######  	/login/login 라는 매핑이 들어왔을경우 put-attribute의 경로에는 *을 {1} 에 넣어줄 수 있음

###### 	/WEB-INF/jsp/login/login.jsp 를 찾아들어감



###### (2) 사용하지않을 menu같은 디자인은 value를 "" 로 입력 , 아예 코드에서 빼도됨

######   2번의 매핑은 로그인을 제외한 **모든루트에 매핑할때** 가능한 구조

######   ex)  /community/community 매핑이 들어올경우 /WEB-INF/jsp/community/community.jsp

######   로 치환. 물론 body의 매핑과 파일명을 맞춰줘야함



###### 보통 톰캣 구동시에 web.xml 의 welcom-file 경로 => 컨트롤러의 @RequestMapping경로를 타는데 타일즈에서 매핑을 쓸수있는 이유는

<property name="order" value="1" />

###### 2번에서 설정한 해당 우선순위 때문

###### 보통은 컨트롤러에서 ViewResolver를 이용해 jsp view를 결정해버리는데 그 우선권을 가로챈 형태



순서를 정리

`url 호출 => @ReqeustMapping => Tiles ViewResolver => UrlBasedViewResolver`



## 4. 3번의 경로에 JSP 생성

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>
<%@ taglib prefix="tiles" uri="http://tiles.apache.org/tags-tiles"%>
<html>
<head>
<title>Example Explosion</title>
<%@ include file="/WEB-INF/include/include-header.jspf" %>
</head>
<body class="wrapper">
    <nav class="navbar navbar-default navbar-static-top" role="navigation" style="margin-bottom: 0">        
        <tiles:insertAttribute name="header"/>        
        <tiles:insertAttribute name="menu" />    
    </nav>
     <div id="page-wrapper">
             <div class="row">
                <div class="col-lg-12">    
                    <h1 class="page-header"></h1>
                </div>
            </div>
            <div class="row">
                
                <tiles:insertAttribute name="body" />                                                  
            </div>          
     </div>
    
 
    
    <div class="main_footer">
        <div class="main_footer-inner">
            <tiles:insertAttribute name="footer" />
        </div>
    </div>
</body>
</html>
```



```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>
<%@ taglib prefix="tiles" uri="http://tiles.apache.org/tags-tiles"%>
 
<html>
<head>
<title>Example Explosion</title>
<%@ include file="/WEB-INF/include/include-header.jspf" %>
</head>
<body>
                
   <tiles:insertAttribute name="body" />                                                 
    
</body>
</html>
```

* ###### include-header.jspf 는 공통 라이브러리들



## 6. Controller

###### view를 해당 파일위치에 맞게 설정

```java
package first.main.controller;
 
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.servlet.ModelAndView;
import first.common.dto.CommandMap;
import first.common.util.ScreenResolver;
 
@Controller
@RequestMapping(value="/main")
public class MainController {
        
    @RequestMapping(value= {"/main","/main.do"})
    public ModelAndView openTilesView(CommandMap commandMap, ModelAndView mv) throws Exception{
        mv.setViewName("/main/main");	//타일즈 view => 일반 view
        mv.addObject("setHeader", ScreenResolver.resolve(this));
        return mv;
    }    
}
```

###### setViewName만 설정해놓으면 title header footer menu 4개는 항상 따라다니며 body의 링크탐