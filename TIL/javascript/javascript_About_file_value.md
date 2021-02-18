# javascript) About file value





```javascript
$("input[type=file]").eq(0).val("")	<= 먹히지 않음

$("input[type=file]").eq(0).prop("defaultValue","") <= 먹힘

=> 안됨 자바스크립트 파일 정책!
```



애초에

```jsp
<input type="file" value="<%=nvl(map, "file_path")"%> 
```



value에 값을 넣지 않고 if문을 이용하여 display만 조작하면 된다.

```jsp
<span class="file_area">
    <%if(!nvl(map, "file_path").equals("")){ %>
        <a href="/주소/입력=<%=URLEncoder.encode(nvl(map, "file_path"), "utf-8") %>&originalFileName=<%=URLEncoder.encode(nvl(map, "file_org_name"), "utf-8") %>" >
            <img src="/이미지/주소.png"/>
            <%=nvl(map, "file_org_name") %>
    	</a>
    <%} %>
</span>
<input type="file" name="file" style="display:<%if(!nvl(file_map, "file_path").equals("")){ out.print("none;");} else { out.print("inline;");} %>">
<span class="file_size" ><%=transFileSize(nvl(map, "file_size")) %></span>
<input type="button" class="file_delete" style="float: right; display:<%if(nvl(map, "file_path").equals("")){ out.print("none;");} else { out.print("inline;");} %>" value="파일삭제"/>
<input type="hidden" name="file_idx" value="<%=nvl(map, "file_idx")%>">	
```

