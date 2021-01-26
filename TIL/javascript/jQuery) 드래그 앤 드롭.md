# jQuery) 드래그 앤 드롭



### 필요한 라이브러리

```html
<link href="https://code.jquery.com/ui/1.12.1/themes/base/jquery-ui.css" rel="stylesheet" type="text/css" />
<script type="text/javascript" src="https://code.jquery.com/jquery-1.12.4.min.js" ></script>
<script type="text/javascript" src="https://code.jquery.com/ui/1.12.1/jquery-ui.js" ></script>
```

###### 가운데 제이쿼리 버전은  높아도 상관 없다.



### 순서 바꾸기 ( 안에서 만 바뀌는)

```html
<div class="sortable-outer">
    <div class="sortable"> 1
        <div>1-1</div>
        <div>1-2</div>
        <div>1-3</div>
        <div>1-4</div>
    </div>
    <div class="sortable"> 2
        <div>2-1</div>
        <div>2-2</div>
        <div>2-3</div>
        <div>2-4</div>
    </div>
</div>
```

```javascript
$(".sortable-outer, .sortable").sortable();
```



### 순서 바꾸기 ( 모든순서)

```html
<div class="sortable">
    <div>1</div>
    <div>1-1</div>
    <div>1-2</div>
    <div>1-3</div>
    <div>1-4</div>
    <div>2</div>
    <div>2-1</div>
    <div>2-2</div>
    <div>2-3</div>
    <div>2-4</div>
</div>
```

```javascript
$(".sortable").sortable();
```



1. ######   뿌릴때 안과 밖을 구분지어 뿌린다 ( ex: style )

2. ######  어케하누... 





