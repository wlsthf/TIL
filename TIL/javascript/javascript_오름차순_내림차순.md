# javascript) 오름차순, 내림차순



```javascript
// 한글 오름차순 내림차순 정렬
let array1 = [
		{name: '영이', idx: 99},
		{name: '철수', idx: 1},
		{name: '민수', idx: 22},
		{name: '강쇠', idx: 8}
	];
array1.sort(function(a, b) { // 숫자 오름차순
	return a.idx - b.idx;  
});
array1.sort(function(a, b) { // 한글 오름차순
	return a.name < b.name ? -1 : a.name > b.name ? 1 : 0;
});
array1.sort(function(a, b) {  // 한글 내림차순
	return a.name > b.name ? -1 : a.name < b.name ? 1 : 0;
});
```





```javascript
// 숫자 정렬
let array2 = [40, 100, 1, 5, 25, 10];
array2.sort(); //[1, 10, 100, 25, 40, 5]
array2.sort(function(a, b){return a-b});  //[1, 5, 10, 25, 40, 100]  //오름차순
array2.sort(function(a, b){return b-a});  //[100, 40, 25, 10, 5, 1]  //내림차순
```





```javascript
// 숫자, 한글 (2가지 조건) 멀티 정렬
let array3 = [
		{name: '가', level: 0},
		{name: '나', level: 0},
		{name: '다', level: 0},
		{name: '라', level: 0},
		{name: '마', level: 0},
		{name: '바', level: 4},
		{name: '사', level: 2}
	];
 
array3.sort(function(a, b) {  
	if(a['level'] === b['level']) { // level값이 같으면 name순 정렬 (레벨값 우선 정렬)
		var x = a['name'].toLowerCase();
		var y = b['name'].toLowerCase();
		return x < y ? -1 : x > y ? 1 : 0;
	}
	return b['level'] - a['level']; 
});
```

