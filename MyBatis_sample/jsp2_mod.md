

# JSP_mod

```jsp
<%@page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8" %>
<%@page extends="BasePage" %>

<%@page import="controller.base.BaseController"%>
<%@taglib prefix="spring" uri="http://www.springframework.org/tags" %>
<%@taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core"%>
<%@taglib prefix="fmt" uri="http://java.sun.com/jsp/jstl/fmt"%>
<%@page import="java.util.*"%>
<%
Map webParameterMap = (Map)request.getAttribute("webParameterMap");
// List list = (List) request.getAttribute("list");

%>

<script >
$(function() {
	
    $("#submit").click(function(){

	    	$("#modify_form").attr("action", "Modify");
	    	$("#modify_form").submit();
	    	
	    	window.opener.location.reload();
	    	window.close();
    
    });
});  

</script>

<div>
	<h1>데이터 수정 팝업</h1>
	<p><a href="javascript:window.close();">X</a></p>

<div>
	<form method="post" id="modify_form">
		<input type="hidden" name="idx" value="${param.idx}">
		<input id="modifyData" name="data" value="${param.data}"/>
		<input type="button" id="submit" value="수정">
	</form>			
</div>
```

