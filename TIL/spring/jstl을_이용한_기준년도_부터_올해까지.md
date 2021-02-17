# jstl을 이용한 기준년도 부터 올해까지 



#### JSP

```jsp
<c:set var="now" value="<%=new java.util.Date()%>" />
<c:set var="this_year"><fmt:formatDate value="${now}" pattern="yyyy"/></c:set>
<select name="년도">
    <c:forEach begin="2020" end="${this_year}" var="year">
        <option value="${year}" ${year eq this_year ? 'selected' : '' }>${year}</option>
    </c:forEach>
</select>
```



#### Mybatis

```xml
<isNotEmpty property="year" prepend="and">
	년도 = #year#
</isNotEmpty>
<isEmpty property="biz_year" prepend="and">
	년도 = EXTRACT(YEAR FROM SYSDATE)
</isEmpty>
```

###### 값이 있으면 해당 연도, 값이 없으면 올해로 설정

###### 조건절에 isNotEmpty, isEmpty 사용







#### 필요한 tablibrary

```jsp
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core"%>
<%@ taglib prefix="fmt" uri="http://java.sun.com/jsp/jstl/fmt"%>
```

