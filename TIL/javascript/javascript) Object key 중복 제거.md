# javascript) Object key 중복 제거

```javascript
list = list.filter(function(item, idx, array) {
	return array.indexOf(item) === idx;
});
```

