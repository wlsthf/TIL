# UUID

###### 범용 고유 식별자(Universally Unique Identifier, UUID)

###### 소프트웨어 구축에 쓰이는 식별자 표준, 분산 컴퓨팅 환경(DCE)의 일부로 표준화

###### iBeacon Advertise 패킷에는 UUID라는 영역있고 생성할 때 특별한 알고리즘을 이용하여 생성

###### UUID 표준에 따라 이름을 부여하면 고유성을 완벽하게 보장할 쑤는 없지만 실제 사용상에서 중복될 가능성이 거의 없다고 인정되기 때문에 많이 사용됨

###### UUID는 16옷텟 (128bit)의 수, 표준 형식에서 UUID는 32개의 16진수로 표현되며 총 36개 문자로 된 8-4-4-4-12라는 5개의 그룹을 하이픈으로 구분

###### ex) 312f6548-a45b-47e6-f234-6554487951236



------

#### 사용법

###### 랜덤한 UUID를 생성하여, 자신의 UUID로 설정

###### Java

```java
UUID uuid1 = UUID.randomUUID();
```



###### Objective C

```objective-c
NSString*uuid = [[NSUUID UUID] UUIDString];
```



###### 웹에서 생성

[UUID 생성]: https://www.guidgenerator.com/
[UUID 생성]: https://www.uuidgenerator.net/





