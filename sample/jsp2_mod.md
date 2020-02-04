

# JSP_mod

```
<%@page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8" %>
<%@page extends="kr.go.moel.efboard.web.admin.util.BasePage" %>

<%@page import="kr.go.moel.efboard.web.admin.controller.base.BaseController"%>
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
	
    $("#bt_submit").click(function(){

	    	$("#modify_form").attr("action", "localCivilComplaintPopupModify");
	    	$("#modify_form").submit();
	    	
	    	window.opener.location.reload();
	    	window.close();
    
    });

});  

</script>

		<div class="popup">
			<h1 class="popup_title">
					데이터 수정 팝업   
			</h1>
			<p class="popup_close"><a href="javascript:window.close();">X</a></p>


			<div class="search" style="padding-bottom:10px;">
				<form method="post" id="modify_form">
					<c:choose>
						<c:when test="${param.column_name == 'col_0'}">
							<select name="data" id="cv_note" style="width:100px;">
								<option value="">지방청</option>
								<option value="12010">서울청</option>
								<option value="13000">부산청</option>
								<option value="14010">대구청</option>
								<option value="15000">중부청</option>
								<option value="16000">광주청</option>
								<option value="17000">대전청</option>
							</select>
							<input type="button" id="bt_submit" value="수정" class="btn01">
						</c:when>
						<c:when test="${param.column_name == 'col_2'}">
							<select name="data" id="cv_value" style="width:100px;">
								<option value="">지방관서</option>

								<c:forEach var="list" items="${list}">
									<option value="${list.cv_value }"  ${list.cv_value eq param.local_name ? 'selected' : '' } >${list.cv_name }</option>
								</c:forEach>								
							</select>							
							<input type="button" id="bt_submit" value="수정" class="btn01">
						</c:when>				
						<c:otherwise>
							<input id="modifyData" name="data" value="${param.data}"/>
							<input type="button" id="bt_submit" value="수정" class="btn01">
						</c:otherwise>	
					</c:choose>
					<input type="hidden" name="record_id" value="${param.record_id}">
					<input type="hidden" name="row_no" value="${param.row_no}">
					<input type="hidden" id="local_name" name="local_name" value="${param.local_name }">
					<input type="hidden" id="col_2" name="column_name" value="${param.column_name}">
					
				</form>
				
			</div>
		</div>
```

