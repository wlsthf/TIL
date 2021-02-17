

# javascript ) XSS / CSRF 공격 가능성 막기

### 필터링 항목



| 태그 | HTML 인코딩 + ; |
| :--: | --------------- |
|  <   | &lt             |
|  >   | &gt             |
|  (   | &#40            |
|  )   | &#41            |
|  #   | &#35            |
|  &   | &#38            |
|  "   | &#quot          |
|  '   | &#39            |



```javascript
/**
 * XSS 공격 방지에 대한 문자 변환을 한다.
 */
onGetEscapeXSS : function (inputText)
{
    var targetText = inputText;
    if (targetText != '' )
    {
        var source = ["&", "<", ">", "\"", "'", "/", "(", ")", "%", "-"];
        var target = ["&amp;","&lt;","&gt;","&quot;","&#39;","&#47;","&#40;","&#41;","&#37;","&#45;"];

        for(var i = 0; i < source.length; i++) {
            targetText = targetText.replace(source[i], target[i]);
        }
    }
    return targetText;
}

/**
 * XSS 공격 방지를 위해 변환된 문자를 원본 문자로 복원한다.
 */
onGetUnescapeXSS : function (inputText)
{
    var plainText = inputText;
    if (plainText != '') {
        var source = ["&amp;","&lt;","&gt;","&quot;","&#39;","&#47;","&#40;","&#41;","&#37;","&#45;"];
        var target = ["&", "<", ">", "\"", "'", "/", "(", ")", "%", "-"];

        for(var  i = 0; i < source.length; i++)  {
            if(plainText.indexOf(source[i]) > -1) {
                plainText = plainText.replace(source[i], target[i]);
            }
        }
    }
    return plainText;
}
```



출처 : [빛나는 리오a 티스토리](https://rios.tistory.com/entry/JS-XSS-CSRF-%EA%B3%B5%EA%B2%A9-%EA%B0%80%EB%8A%A5%EC%84%B1-%EB%A7%89%EA%B8%B0%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8?category=711004)

