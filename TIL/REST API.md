# REST API

###### REST는 Representational State Transfer약자이며 HTTP(웹) 설계의 우수성에 비해 제대로 사용되어지지 못해 안타까워하며 웹에 장점을 최대한 활용할 수 있는 아키텍처로써 REST를 발표했다. ( 로이 필딩 ) 

 

## REST 구성

##### 자원 (RESOURCE) : URI 

##### 행위(Verb) : HTTP METHOD 

##### 표현 (Representations)  : JSON

 

## REST 특징

1. ##### Uniform (유니폼 인터페이스) 

   ###### 유니폼 인터페이스는 URI로 지정한 리소스에 대한 조작을 통일되고 한정적인 인터페이스로 수행하는 아키텍처 스타일을 말한다. 

2. ##### Stateless (무 상태성) 

   ###### REST는 무 상태성 성격을 가지고있다. 다시 말해 작업을 위한 **상태정보를 따로 저장하고 관리하지 않는다.** 세션 정보나 쿠키 정보를 별도로 저장하고 관리하지 않기 때문에 API 서버는 들어오는 요청 만을 단순히 처리하면 된다. 때문에 서비스의 자유도가 높아지고 서버에서 불필요한 정보를 관리하지 않음으로써 구현이 단순해진다.

3. ##### Cacheable (캐시 가능) 

   ###### REST의 가장 큰 특징 중 하나는 HTTP라는 기존 웹 표준을 그대로 사용하기 때문에, 웹에서 사용하는 기존 인프라를 그대로 활용이 가능하다. 따라서 HTTP가 가진 캐싱 기능이 적용이 가능합니다. HTTP 프로토콜 표준에서 사용하는 Last-Modified태그나 E-Tag를 이용하면 캐싱 구현이 가능하다.

4. ##### Self-descriptiveness (자체 표현 구조)

   ###### REST의 또 다른 큰 특징 중 하나는 REST API만 보고도 이를 쉽게 이해 할 수 있는 자체 표현 구조로 되어 있다

5. ##### Client – Server 구조 

   ###### REST 서버는 API제공, 클라이언트는 사용자 인증이나 컨텍스트(세션,로그인 정보)등을 직접 관리하는 구조로 각각의 역할이 확실하게 구분되기 때문에 클라이언트와 서버에서 개발해야 할 내용이 명확해지고 서로간 의존성이 줄어들게 된다.

6. ##### 계층형 구조 

   ###### REST 서버는 다중 계층으로 구성될 수 있으며 보안, 로드밸런싱, 암호화 계층을 추가해 구조상의 유연성을 둘 수 있고 PROXY, 게이트웨이 같은 네트워크 기반의 중간 매체를 사용할 수 있게 한다.

 

## REST API 디자인 가이드

- ##### URI는 정보의 자원을 표현해야한다.

- ##### 자원에 대한 행위는 HTTP Method(GET,POST,PUT,DELETE)로 표현한다.

 

### REST API 중심 규칙

- ##### URI는 정보의 자원을 표현해야한다. (리소스 명은 동사보단 명사를 사용) 

  ###### 	GET /member/delete/1  X

  ###### 	- 위와 같이 delete와 같은 행위에 대한 표현을 들어가서는 안된다. 

- ##### 자원에 대한 행위는 HTTP Method로 표현 

  ###### 	DELETE /member/1** O

  ###### 	회원정보를 가져올땐 GET ,회원 추가 표현은 POST 등을 사용하여 표현 

 

### [참고]HTTP METHOD의 알맞은 역할

###### POST, GET, PUT, DELETE 이 4가지의 메소드를 가지고 CRUD를 할수 있다. 

| METHOD | 역할                                                         |
| ------ | ------------------------------------------------------------ |
| POST   | POST를 통해 해당 URI를 요청하면 리소스를 생성                |
| GET    | GET를 통해 해당 리소스를 조회. 리소스를 조회하고 해당 도큐먼트에 대한 자세하 정보를 가져온다. |
| PUT    | PUT를 토해 리소스 수정                                       |
| DELETE | DELETE를 통해 리소스를 삭제                                  |

 

### URI 설계시 주의할 점

1. ##### 슬래쉬 구분자(/)는 계층 관계를 나타내는데 사용 

   ###### 	http://test.example.com/houses/apartments 

   ###### 	http://test.eample.com/animals/mammals/wales 

2. ##### URI 마지막 문자로 /를 포함하지 않음

   ###### URI에 포함되는 모든 글자는 리소스의 유일한 식별자로 사용되어야 하며 URI가 다르다는 것ㄷ은 리소스가 다르다는 것이고, 역으로 리소스가 다르면 URI도 달라져야 한다. REST API는 분명한 URI를 만들어 통신을 해야하기 때문에 혼동을 주지않도록 URI 경로의 마지막에는 /를 사용하지 않는다.

   ###### http://test.example.com/houses/apartments/ X

3. ##### 하이픈(-)은 URI의 가독성을 높이는데 사용 

   ###### URI를 쉽게 읽고 해석하기위해 불가피하게 긴 URI경로를 사용하게 된다면 –를 사용하여 가독성을 높일 수 있다.

4. ##### 밑줄(_)은 URI에사용하지 않음

5. ##### 가독성 때문에 소문자가 적합

   ###### 대소문자에 따라 다른 리소스로 인식하기 때문에 RFC3986(URI 문법 형식)은 URI 스키마와 호스트를 제외하고는 대소문자를 구별하도록 규정하기 때문이다.

6. ##### 파일확장자는 포함시키지 않는다.

   ###### REST API에서는 메시지 바디 내용의 포맷을 나타내기 위한 파일확장자를 URI 안에 포함시키지 않는다. Accept header를 사용!

   ###### GET / members/soccer/345/photo HTTP/1.1 Host: test.example.com Accept: image/jpg 

   

### 리소스 간의 관계를 표현하는 방법

##### REST 리소스 간에는 연관 관계가 있을 수 있고 이런경우 다음과 같은 표현방법으로 사용

###### 	/리소스명/리소스 ID/관계가있는 다른 리소스명 

###### 	ex) GET : /users/{userid}/devices 

###### 만약에 관계명이 복잡하다면 이를 서브 리소스에 명시적으로 편현하는 방법이 있다.

###### 예를들어 사용자가 '좋아하는' 디바이스 목록을 표현해야 할 경우 다음과 같다.

######         GET : /user/{userid}/likes/devices 



### 자원을 표현하는 Collection과 Document

###### Collection과 Document에 대해 알면 URI설계까 한 층 더 쉬워진다. Document는 단순히 문서로 이해해도 되고, 한 객체라고 이해해도 된다. 컬렉션은 문서들의 집합, 객체들의 집합이라고 생각하면 된다.

######         http://restapi.com/sports/soccer 

###### 위 URI를 보면 스포츠라는 컬렉션과 사커라는 도큐먼트로 표현

######         http://restapi.com/sports/soccer/players/13 

###### sports,players 컬렉션과 soccer,13 를 의미하는 도큐먼트로 URI이루어지게된다.

###### 여기서 중요한점은 컬렉션은 복수로 사용하는 것이다. 좀 더 직관적인 REST API를 위해서는 컬레렉션과 도큐먼트를 사용할 때 단수 복수도 지켜준다면 좀더 이해하기 쉬운 URI를 설계할 수 있다.



### HTTP 응답 상태 코드

###### 잘 설계된 REST API는 URI만 잘설계된 것이 아닌 그 리소스에 대한 응답을 잘 내어주는 것까지 포함되어야 한다.

###### 정확한 응답의 상태코드만으로도 많은 정보를 전달할 수가 있기 때문이다.

| 상태코드 |                                                              |
| -------- | ------------------------------------------------------------ |
| 200      | 클라이언트의 요청을 정상적으로 수행                          |
| 201      | 클라이언트가 어떠한 리소스를 생성을 요청, 해당 리소스가 성공적으로 생성됨 <br>(POST를 통한 리소스 생성 작업시) |
| 상태코드 |                                                              |
| 400      | 클라이언트의 요청이 부적절 할 경우 사용하는 응답 코드        |
| 401      | 클라이언트가 인증되지 않은 상태에서 보호된 리소스를 요청했을 때 사용하는 응답코드 <br> (로그인 하지 않은 유저가 로그인 했을 때, 요청 가능한 리소스를 요청했을 때) |
| 403      | 유저 인증상태와 관계 없이 응답하고 싶지 않은 리소스를 클리아언트가 요청했을 때 사용 |
|          | (403 보다는 400이나 404를 사용할 것을 권고 403 자체가 리소스가 존재한다는 뜻이기 때문) |
| 405      | 클라이언트가 요청한 리소스에서는 사용 불가능한 Method를 이용했을 경우 사용하는 응답코드 |
| 상태코드 |                                                              |
| 301      | 클라이언트가 요청한 리소스에 대한 URI가 변경 되었을 때 사용하는 응답코드 <br>(응답시 Location header에 변경된 URI를 적어 줘야한다) |
| 500      | 서버에 문제가 있을경우 사용하는 응답코드                     |

 

### Spring에서 RESTFUL API 적용

```java
@RestController
public class RestAPITestController {

	@RequestMapping(value =”/test”,method = RequestMethod.GET)
	public RestTest testRestAPI(){
		RestTest test new RestTest(); //VO
		test.setName(”KYS”);
		test.setAge(4);
		test.setCurrentTime(LocalDateTime.now().toString());
		return test;
	}
}
```

###### 여기서 @RestController를 보면, @RestController는 스프링4.0부터 나온것으로 @Controller와 @ ResoponseBody를 합쳐 놓은것이다 @Controller를 이용하여 Restful API를 만들려면 아래 코드처럼 @ResponseBody를 붙여야한다.  

```java
@Controller
public class RestAPITestController {

	@RequestMapping(value =”/test”,method = RequestMethod.GET)
	public @ResponseBody RestTest testRestAPI(){
		RestTest test new RestTest(); //VO
		test.setName(”KMS”);
		test.setAge(25);
		test.setCurrentTime(LocalDateTime.now().toString());
		return test;
	}
}
```



 

#### GET

```java
@RequestMapping(value = "/customer", method = RequestMethod.GET) 
public ResponseEntity<List<Customer>> listAllCustomers() {
	final List<Customer> allCustomers = customerService.findAllCustomers();
	if (allCustomers.isEmpty()) {
		return new ResponseEntity<List<Customer>>(HttpStatus.NO_CONTENT);
	}
	
	return new ResponseEntity<List<Customer>>(allCustomers, HttpStatus.OK);
}
@RequestMapping(value = "/customer/{id}", method = RequestMethod.GET)
public ResponseEntity<Customer> getCustomer(@PathVariable("id") final Long id) {
	final Customer fetchedCustomer = customerService.findById(id);
	if (fetchedCustomer == null) {
		return new ResponseEntity<Customer>(HttpStatus.NOT_FOUND);
	}
	return new ResponseEntity<Customer>(fetchedCustomer, HttpStatus.OK);
```

 

###### 위에서 보면 전체 customer list를 가져오거나 @PathVariable을 이용하여 customer ID 를 보내 특정 customer 를 검색하여 데이타를 받는 경우이다. method = RequestMethod.GET 을 @RequestMapping 에 정의 하면 된다. 리턴은 ReponseEntity<T> 클래스를 이용하여 검색이 되지 않았을 경우에는 HttpStatus.NOT_FOUND 를 넘겨 주고, 검색이 되었을 경우에는 검색한 결과 object을 HttpStatus.OK 와 함께 넘겨 준다. 이때 Spring 에서는 자동으로 jackson-databind 를 이용하여 JSON 포맷으 데이타를 넘겨 준다. 

 

#### POST

```java
@RequestMapping(value = "/customer", method = RequestMethod.POST)
public ResponseEntity<Void> createCustomer(@RequestBody final Customer customer,
		final UriComponentsBuilder ucBuilder) {
	
	if (customerService.isCustomerExist(customer)) {
		return new ResponseEntity<Void>(HttpStatus.CONFLICT);
	}
	final Customer savedCustomer = customerService.saveCustomer(customer);
	
	final HttpHeaders headers = new HttpHeaders();
	headers.setLocation(ucBuilder.path("/customer/{id}").buildAndExpand(savedCustomer.getId()).toUri());
	return new ResponseEntity<Void>(headers, HttpStatus.CREATED);
}
```

 

###### POST 는 새로운 Data를 생성 할 때 사용 하는 방법으로 method = RequestMethod.POST 로 설정을 해 준다. argument 들로 Customer 객체를 @RequestBody 를 이용하여 받아 왔다. Front-end 쪽에서 JSON 포맷으로 Customer 데이타를 보내 주면 된다. 이 떄 Front-end 개발자는 POST 이기 때문에 새로운 객체를 생성해야 하는 것으로 알고 데이타를 보내 주어야 한다. 두번 째 argument 로 UriComponentBuilder 를 설정 했다. 이유는 Customer를 생성하고 HttpHeaders 객체의 location 정보를 넣어 주기 위함이다. 이렇게 해 주면 Front-end 쪽 개발자는 새로운 데이타가 성공적으로 생성 (HttpStatus.CREATED) 되었을 경우 header 정보에서 location 값을 찾아 redirect 해 줄 수 있게 된다. 

###### 위에서 보면 만약 새롭게 생성하려고 하는 데이타가 이미 존재 하는 경우라면 HttpStatus.CONFLICT를 ResponseEntity<Void> 를 통해 리턴해 준다. 

  

#### PUT

```java
@RequestMapping(value = "/customer/{id}", method = RequestMethod.PUT)
public ResponseEntity<Customer> updateCustomer(@PathVariable("id") final Long id,
		@RequestBody final Customer customer) {
	final Customer updatedCustomer = customerService.updateCustomer(id, customer);
	
	if (updatedCustomer == null) {
		return new ResponseEntity<Customer>(HttpStatus.NOT_FOUND);
	}
	
	return new ResponseEntity<Customer>(updatedCustomer, HttpStatus.OK);
}
```

  

##### PATCH

```java
@RequestMapping(value = "/customer/{id}", method = RequestMethod.PATCH)
public ResponseEntity<Customer> patchCustomer(@PathVariable("id") final Long id,
		@RequestBody final Customer customer) {
	final Customer patchedCustomer = customerService.patchCustomer(id, customer);
	
	if (patchedCustomer == null) {
		return new ResponseEntity<Customer>(HttpStatus.NOT_FOUND);
	}
	
	return new ResponseEntity<Customer>(patchedCustomer, HttpStatus.OK);
}
```

 

###### 위에서 method = RequestMethod.PATCH 를 설정해 주었고 업데이트 하려는 Customer의 ID와 Customer 객체를 받았다. 받은 Customer 객체의 경우 실제 업데이트 하려는 property 에만 값이 들어 있고 나머지는 null 이 들어 있게 된다. PATCH 가 성공적으로 되었으면 업데이트된 Customer 와 HttpStatus.OK 를 ResponseEntity<Customer> 에 넣어 보내 주고, 그렇지 않을 경우에는 HttpStatus.NOT_FOUND 를 넘겨준다.  

 





#### DELETE

```java
@RequestMapping(value = "/customer/{id}", method = RequestMethod.DELETE)
public ResponseEntity<Void> deleteCustomer(@PathVariable("id") final Long id) {
	Boolean deleteResult = customerService.deleteCustomer(id);
	
	if (deleteResult == null || !deleteResult) {
		return new ResponseEntity<Void>(HttpStatus.NOT_FOUND);
	}
	
	return new ResponseEntity<Void>(HttpStatus.OK);
}
```

 

###### method = RequestMethod.DELETE 를 이용 하고 성공했을 경우 ResponseEntity<Void> 에 HttpStatus.OK 를 넣어 주고 그렇지 않을 경우 HttpStatus.NOT_FOUND 를 넣어 넘겨주었다. 

 

 

##### <u>스프링으로 프로젝트를 만들어서 디비연결을 다했다면 POSTMAN으로 테스트</u>

##### <u>혹은 test코드 작성을 통해서 확인</u>