# javascript) 엔터 폼 서브밑 막기

```javascript
document.addEventListener('keydown', function(event) {
  if (event.keyCode === 13) {
    event.preventDefault();
  };
}, true);
```

