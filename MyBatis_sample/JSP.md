# JSP

```jsp
<%@page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8" %>
<%@page extends="kr.go.moel.efboard.web.admin.util.BasePage" %>
<%@page import="kr.go.moel.efboard.web.admin.controller.base.BaseController"%>
<%@taglib prefix="spring" uri="http://www.springframework.org/tags" %>
<%@page import="java.util.*"%>

<%
Map webParameterMap = (Map)request.getAttribute("webParameterMap");
List<Map> list		= (List)request.getAttribute("list");
%>

<form method="post" id="regist_form" enctype="multipart/form-data">
	</table>
    	<table>
        <thead>
			<tr>
            	<th colspan="3">제목</th>
            </tr>
            <tr>
                <th>부제1</th>
                <th colspan="2">부제2</th>
			</tr>
            <tr>
            	<th>컬럼1</th>
                <th>컬럼2</th>
                <th>컬럼3</th>
			</tr>
		</thead>
<%
        if(list != null) {	
			for(int i=0; i<list.size(); i++){
                    Map map = list.get(i);
%>
			<tr>
            	<input type="hidden" name="idx" value="<%=nvl(map, "idx")%>">
                <td onclick="modifyData(<%=nvl(map, "id")%>, 'col_1', <%=nvl(map, "col_1") %>">
                    <%=nvl(map,"col_1")%>
                </td>
                <td onclick="modifyData(<%=nvl(map, "id")%>, 'col_2', <%=nvl(map, "col_2") %>">
                    <%=nvl(map,"col_2")%>
                </td>
                <td onclick="modifyData(<%=nvl(map, "id")%>, 'col_3', <%=nvl(map, "col_3") %>">
                    <%=nvl(map,"col_3")%>
                </td>
                <th>
                    <input type="button" value="삭제" class="btn04 delRowData" onclick="delRowAjax(<%=nvl(map, "record_id")%>, <%=nvl(map, "row_no")%>)">
                </th> 
            </tr>
<%
			}
		}
%>

	</table>
</form>

<div>
    <div>
        <input type="button" id="regist_btn" value='등록'/>
    </div>

</div>
```

