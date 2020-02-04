# JSP

```jsp
<%@page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8" %>
<%@page extends="kr.go.moel.efboard.web.admin.util.BasePage" %>
<%@page import="kr.go.moel.efboard.web.admin.controller.base.BaseController"%>
<%@taglib prefix="spring" uri="http://www.springframework.org/tags" %>
<%@page import="java.util.*"%>

<%
Map webParameterMap = (Map)request.getAttribute("webParameterMap");
List<Map> listPopup  = (List)request.getAttribute("list");
%>

<div class="order_area">
  <h3 class="order_title"><strong>민원 현황 데이터 관리</strong></h3>
  <div class="write">
      <form method="post" id="regist_form" enctype="multipart/form-data">

        <!-- 컬럼추가 -->
        <table class="write_table mgt30">
          <thead>
          <tr>
            <th><strong>지방 관서별 민원 처리 현황 데이터 등록</strong></th>
            <td><input type="text" id="addRowCnt_1"/></td>
            <th><input type="button" id="addRow_1" class="btn04" value="추가" /></th>
          </tr>
          </thead>
        </table>
          <table id="tblExport" class="write_table" style="border="0"; cellspacing="0";>
            <thead>
            <tr>
              <tr>
                <th colspan="6">국민신문고</th>
				<th rowspan="3"></th>
              </tr>
              <tr>
                <th colspan="2">기관명</th>
                <th colspan="4"></th>
			  </tr>
				<th>지방청</th>
                <th>지방관서</th>
                <th> 접수 </th>
                <th> 처리 </th>
                <th> 처리대상민원</th>
                <th> 처리기한도과민원</th>
			  </tr>
              </thead>
<%
            if(listPopup != null) {	
                for(int i=0; i<listPopup.size(); i++){

                    Map map = listPopup.get(i);
%>
			  <tr><input type="hidden" name="idx" value="<%=nvl(map, "local_civil_complaint_idx")%>">
              <input type="hidden" class="row_no" value="<%=nvl(map, "row_no")%>">
                <td style="cursor:pointer;" onclick="modifyData(<%=nvl(map, "record_id")%>, <%=nvl(map, "row_no")%>, '<%=nvl(map, "col_0") %>', 'col_0', <%=nvl(map, "col_0") %>)"><%=nvl(map,"local_name")%></td>
                <td style="cursor:pointer;" onclick="modifyData(<%=nvl(map, "record_id")%>, <%=nvl(map, "row_no")%>, '<%=nvl(map, "col_2") %>', 'col_2', <%=nvl(map, "col_0") %>)"><%=nvl(map,"local_office_name")%></td>
                <th><input type="button" value="삭제" class="btn04 delRowData" onclick="delRowAjax(<%=nvl(map, "record_id")%>, <%=nvl(map, "row_no")%>)">
                </th> 
            </tr>
            <%
            	}
            }
            %>

            <tbody id="columnBody">

            </tbody>

            </table>
        </form>
</div>

<div class="btn_both">
    <div class="fl">
        <!-- <input type="button"  id="btn_delete" class="btn02" value="삭제"> -->
        <input type="button"  id="btn_reset" class="btn01" value="초기화">
        <a id="btnExport" href="#" download="">
            <input type="button"  id="btn_excel" class="btn01" value="엑셀">
        </a>
        <input type="button" id="regist_btn" class="btn03" value='등록'/>
        <!-- <input type="button" id="apply_btn" class="btn03" value='적용'/> -->
    </div>
    <div class="fr">
    </div>
</div>

</div>
```

