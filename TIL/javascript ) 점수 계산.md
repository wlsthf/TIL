# javascript ) 점수 계산

##### javascript

```javascript
$(function(){
	
	// 총점
	$(".evaluateTb :text").keyup(function() {										
	//alert("함수 접근 성공!");
		var $this = $(this);
		var type = $this.parent().parent().parent().parent().attr("id"); 			
		//alert("테이블 타입 : " + type);
		var $total = $("#" + type + " .total");
		var total = Number($total.text()); 											
		//alert("총점은 : " + total);			
		var score = Number($this.val());											
		//alert("입력한 점수는 : " + score);					
		var test = isNaN(score);													
		//alert("숫자가 아닙니까 : " + test);
		var maxScore = Number($this.parent().siblings().eq(1).text().substr(0,2));	
		//alert("입력한 점수의 최대 점수는 : " + maxScore);
		var item = $this.parent().siblings().eq(0).text();							
		//alert("항목의 이름 : " + item);
		var scoreCnt = $("#" + type + " tr").length -3; 	//점수가 들어가는 tr 이외의 tr제외	
		//alert("평가항목의 갯수 : "scoreCnt);
		
		// 숫자 검사
		if(test) {
			alert("숫자를 입력해주세요.");
			$this.val("");
			$this.focus();
			//return false;	//값이 반영되지 않음.
		}
		
		// 점수 범위 검사
		if(score < 0) {
			alert("0점 이상을 입력해 주세요");
			$this.val("");
			$this.focus();
			//return false;
		} else if (score > maxScore) {
			alert(item + "의 최대 점수는 " + maxScore + "입니다.");
			$this.val("");
			$this.focus();
			//return false;
		}
		
 		total = 0;
 		
		for (var i = 1; i <= scoreCnt; i++) {
			var sum = Number($("#" + type + "_" + i).val());								
			//console.log(i + "번째 값 : " + sum);
			
			total += sum
		} 
		
		$total.text(total);
	});		
});
```





HTML

```html
<!--첫번째 테이블 영역 시작-->
<table class="evaluateTb" id="docEv">
    <thead>
        <tr>
            <th>항목이름</th>
            <th>배점</th>
            <th>항목설명</th>
            <th>배점</th>	
        </tr>
    </thead>
    <tbody>
        <tr>
            <th>항목1</th>
            <td>10점</td>
            <td>항목1의 설명입니다.</td>
            <td>
                <input type="text" id="docEv_1"/><span>10</span>			
            </td>
        </tr>
        <tr>
            <th>항목2</th>
            <td>30점</td>
            <td>항목2의 설명입니다.</td>
            <td>
                <input type="text" id="docEv_2"/><span>30</span>			
            </td>
        </tr>
        <tr>
            <th>항목3</th>
            <td>20점</td>
            <td>항목3의 설명입니다.</td>
            <td>
                <input type="text" id="docEv_3"/><span>20</span>			
            </td>
        </tr>
        <tr>
            <th>항목4</th>
            <td>20점</td>
            <td>항목4의 설명입니다.</td>
            <td>
                <input type="text" id="docEv_4"/><span>20</span>			
            </td>
        </tr>
        <tr>
            <th>항목5</th>
            <td>20점</td>
            <td>항목5의 설명입니다.</td>
            <td>
                <input type="text" id="docEv_5"/><span>20</span>			
            </td>
        </tr>
        <tr>
            <th>합계</th>
            <th>100점</th>
            <th></th>
            <th><span class="total"></span>/100</th>
        </tr>
        <tr>
            <th colspan="2">종합 평</th>
            <td colspan="2">
                <textarea rows="4"></textarea>
            </td>
        </tr>
    </tbody>
</table>
<!-- 첫번째 테이블 영역 끝 -->


<!-- 두번째 테이블 영역 시작 -->
<table class="evaluateTb" id="ptEv">
    <thead>
        <tr>
            <th>항목이름</th>
            <th>배점</th>
            <th>항목설명</th>
            <th>배점</th>	
        </tr>
    </thead>
     <tbody>
        <tr>
            <th>항목1</th>
            <td>10점</td>
            <td>항목1의 설명입니다.</td>
            <td>
                <input type="text" id="ptEv_1"/><span>10</span>			
            </td>
        </tr>
        <tr>
            <th>항목2</th>
            <td>30점</td>
            <td>항목2의 설명입니다.</td>
            <td>
                <input type="text" id="ptEv_2"/><span>30</span>			
            </td>
        </tr>
        <tr>
            <th>항목3</th>
            <td>20점</td>
            <td>항목3의 설명입니다.</td>
            <td>
                <input type="text" id="ptEv_3"/><span>20</span>			
            </td>
        </tr>
        <tr>
            <th>항목4</th>
            <td>20점</td>
            <td>항목4의 설명입니다.</td>
            <td>
                <input type="text" id="ptEv_4"/><span>20</span>			
            </td>
        </tr>
        <tr>
            <th>항목5</th>
            <td>20점</td>
            <td>항목5의 설명입니다.</td>
            <td>
                <input type="text" id="ptEv_5"/><span>20</span>			
            </td>
        </tr>
        <tr>
            <th>합계</th>
            <th>100점</th>
            <th></th>
            <th><span class="total"></span>/100</th>
        </tr>
        <tr>
            <th colspan="2">종합 평</th>
            <td colspan="2">
                <textarea rows="4"></textarea>
            </td>
        </tr>
    </tbody>
</table>
<!--두번째 테이블 영역 끝-->
```

