# javascript) object key 정렬

```javascript
var unOrdered = {
  'b': 'foo',
  'c': 'bar',
  'a': 'baz'
};
var ordered = new Object();	

Object.keys(unOrdered).sort().forEach(function(key) {
    ordered[key] = unOrdered[key];
});
		
```

