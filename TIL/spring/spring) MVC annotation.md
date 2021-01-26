# spring) MVC annotation

```java
@RestController 	// @Controller + @ResponseBody
@GetMapping("uri") = @RequestMapping(value = "/uri", method = RequestMethod.GET)
@PostMapping, @PatchMapping, @PutMapping, @DeleteMapping
@ResponseEntity 	// 본문 응답 이외에 HTTP 헤더와 상태코드 제어 기능 제공
@RepuestParam 		// API의 URI 쿼리 매개변술르 지정하는 기능 제공
@PathVariable 		// /users/{userId}에서 userId같이 URI 변수를 추출하는 기능 제공
    
// + Spring HATEOAS!!
```

