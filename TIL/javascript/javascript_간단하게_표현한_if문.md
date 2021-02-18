# javascript) 간단하게 표현한 if문



```javascript
// 방법1
true && console.log("된다!");

// 방법2
2 === 2 && (console.log("된"), console.log("다"));

// 방법3
3 === 3 && function() {
    console.log("된");
    console.log("다");
}();
```

