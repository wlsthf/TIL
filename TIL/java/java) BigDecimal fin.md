# java) BigDecimal fin



## BigDecimal과 Java Stream

```java
// POJO 목록에서 BigDecimal 타입을 가진 특정 필드의 합을 반환
BigDecimal sumOfFoo = fooList.stream()
    .map(FooEntity::getFooBigDecimal)
    .filter(foo -> Objects.nonNull(foo))
    .reduce(BigDecimal.ZERO, BigDecimal::add);

// 특정 BigDecimal 필드를 기준으로 오름차순 정렬된 리스트를 반환
foolist.stream()
    .sorted(Comparator.comparing(it -> it.getAmount()))
    .collect(Collectors.toList());

// 위와 동일한 기능, 정렬된 새로운 리스트를 반환하지 않고 원본 리스트를 바로 정렬
foolist.sort(Comparator.comparing(it -> it.getAmount()));
```



## AtomicBigDecimal

> - **Google Guava**는 서로 다른 쓰레드에서 하나의 **double** 변수에 접근시 동시성을 보장하는 `com.google.common.util.concurrent.AtomicDouble`을 제공한다. 현재까지, **AtomicBigDecimal**은 제공되지 않는데 필요할 경우 `java.util.concurrent.atomic.AtomicReference`를 이용하여 아래와 같이 구현할 수 있다.

```java
package com.jsonobject.example;

import java.math.BigDecimal;
import java.util.concurrent.atomic.AtomicReference;

public class AtomicBigDecimal {

    private final AtomicReference<BigDecimal> valueHolder = new AtomicReference(BigDecimal.ZERO);

    public AtomicBigDecimal() {
    }

    public AtomicBigDecimal(BigDecimal initialValue) {

        valueHolder.set(initialValue);
    }

    public AtomicBigDecimal(double initialValue) {

        this(BigDecimal.valueOf(initialValue));
    }

    public BigDecimal get() {

        return valueHolder.get();
    }

    public void set(BigDecimal initialValue) {

        valueHolder.set(initialValue);
    }

    public BigDecimal addAndGet(BigDecimal delta) {

        return valueHolder.updateAndGet(x -> x.add(delta));
    }

    public BigDecimal addAndGet(double delta) {

        return this.addAndGet(BigDecimal.valueOf(delta));
    }

    public BigDecimal getAndAdd(BigDecimal delta) {

        return valueHolder.getAndUpdate(x -> x.add(delta));
    }

    public BigDecimal getAndAdd(double delta) {

        return this.getAndAdd(BigDecimal.valueOf(delta));
    }

    public double doubleValue() {

        return this.get().doubleValue();
    }

    public String toString() {

        return this.get().toString();
    }
}
```



## BigDecimal 타입의 JSON 문자열 변환

> - 지금까지 알아본 **BigDecimal**의 애플리케이션 내부 연산과 저장소 말고도 신경 써야 할 것이 있다. 바로, 외부 서비스 간의 **API** 요청-응답 처리이다. **JSON** 스펙에서는 **BigDecimal** 타입의 표현 방법에 대해 명확히 규정하고 있지 않다. 그래서 **API** 응답을 표현할 때 혹시 모를 소수점 이하에서의 데이터 유실을 확실하게 예방하려면 **BigDecimal**을 숫자가 아닌 문자열로 응답해야 한다. [[관련 링크\]](https://stackoverflow.com/questions/52149589/return-bigdecimal-fields-as-json-string-values-in-java) 아래는 **Jackson** 라이브러리를 사용하여 **POJO-JSON** 변환시 소수점 이하 6자리에서 **Bankers Rounding**을 적용하여 응답하는 커스텀 **JsonSerializer**를 제작한 예이다.

```java
class BigDecimalScale6WithBankersRoundingSerializer : JsonSerializer<BigDecimal>() {

    companion object {

        const val SCALE_SIX = 6
        val BANKERS_ROUNDING_MODE = RoundingMode.HALF_EVEN
    }

    override fun serialize(value: BigDecimal?, gen: JsonGenerator?, serializers: SerializerProvider?) {

        gen?.writeString(value?.setScale(SCALE_SIX, BANKERS_ROUNDING_MODE).toString())
    }
}
```

- 앞서 제작한 **JsonSerializer**를 아래와 같이 **POJO**에 명시하면 의도한대로 **JSON** 응답 처리를 할 수 있다.

```java
@JsonSerialize(using = BigDecimalScale6WithBankersRoundingSerializer::class)
var fooDecimal: BigDecimal? = BigDecimal.ZERO,
```



## BigDecimal 유닛 테스트

> - **BigDecimal**은 **JUnit**에서 **Assertion** 기능을 제공하지 않아 유닛 테스트가 불편하다. `AssertJ` 라이브러리를 이용하면 아래와 같이 네이티브하게 **BigDecimal**에 대한 유닛 테스트를 수행할 수 있다. [[라이브러리 링크\]](https://joel-costigliola.github.io/assertj/)

```java
BigDecimal a = BigDecimal.valueOf(0.1);
BigDecimal b = BigDecimal.valueOf(0.10);
BigDecimal c = BigDecimal.valueOf(0.101);
BigDecimal d = BigDecimal.valueOf(0.001);

// equals()와 동일하기 때문에 소수점 마지막 0까지 동일해야 true
// false
assertThat(a).isEqualTo(b));

// compareTo()와 동일하기 때문에 소수점 마지막 0이 달라도 true
// true
assertThat(a).isEqualByComparingTo(b);

// 두 수가 주어진 오차 범위를 만족하면 true
// true
assertThat(a).isCloseTo(c, within(d));
```



## BigDecimal 관련 라이브러리

> - `big-math` 라이브러리는 **java.lang.Math** 클래스의 **BigDecimal** 버전이라고 할 수 있다. **BigDecimal** 기반 연산과 관련된 여러 유용한 기능을 제공한다. [[라이브러리 링크\]](https://github.com/eobermuhlner/big-math)



## BigDecimal과 통화

> - **BigDecimal**은 돈을 다루는데 있어 가장 확실하고 안전한 타입이다. 하지만, 여러 국가의 통화를 표현하기에는 부족함이 있다. 이러한 통화를 다루기 위한 **Java** 표준으로 **JSR 354**가 존재한다. 그리고 이를 구현한 구현체 라이브러리로 `Moneta`가 존재한다. 여러 국가의 통화를 직접 처리하는 것보다 이러한 정식 구현체를 적용하는 것이 효율적이다. [[라이브러리 링크\]](http://javamoney.github.io/ri.html)
> - 아래는 **build.gradle**에 해당 라이브러리의 종속성을 추가하는 방법이다.

```java
compile group: 'org.javamoney', name: 'moneta', version: '1.3', ext: 'pom' // JavaMoney
compile group: 'org.javamoney.lib', name: 'javamoney-lib', version: '1.0', ext: 'pom' // JavaMoney
compile group: 'org.javamoney.lib', name: 'javamoney-calc', version: '1.0' // JavaMoney Caculations
```

