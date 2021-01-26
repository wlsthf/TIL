# java) BigDecimal 사용법 정리

###### PostgreSQL 에서 배열을 넣고 빼는 작업중 _numeric 컬럼에서 자바로 넘어 올때 BigDecimal 로 넘어와서 (Double은 사용 못함..)  사용법을 찾아보던중 좋은 자료 발견!



## BigDecimal

######  java에서 숫자를 정밀하게 표현하고 저장할 수 있는 유일한 방법!

###### 돈과 소수점을 다룬다면 꼭 BigDecimal로 하자



## Double의 문제점

###### Double은 10진수 => 2진수 => 10진수 형태로 저장/출력하기 때문에 사칙연산등에서 오류가 발생할 수 있다.



## BigDecimal 기본 용어

- ###### precision: 숫자의 전체 자리수 unscale과 동의어 (앞뒤의 무의미한 0은 계산 x)

- ###### scale: 전체 소수점 자리수 (무의미한 0은 계산 x)

- ###### DECIMAL128: **IEEE 754-2008**에 의해 표준화된, 부호와 소수점을 수용하며, 최대 34자리까지 표현 가능한 10진수를 저장할 수 있는 형식. 2018년 미국 정부의 총 부채액이 15조 7천 500억 달러로 총 14자리 임을 감안하면, 금융권에서 처리되는 대부분의 금액을 수용할 수 있는 크기. **Java**에서는 **BigDecimal** 타입을 통해 공식적으로 지원



## BigDecimal 기본 상수

> 초기화가 장황 하기때문에 자주쓰는 수는 미리 상수로 정의

```java
// 흔히 쓰이는 값은 상수로 정의
// 0
BigDecimal.ZERO

// 1
BigDecimal.ONE

// 10
BigDecimal.TEN
```



## BigDecimal 초기화

> 문자열의 형태로 초기화 하는것이 숫자의 유실을 막는다

```java
// double 타입을 그대로 초기화하면 기대값과 다른 값을 가진다.
// 0.01000000000000000020816681711721685132943093776702880859375
new BigDecimal(0.01);

// 문자열로 초기화하면 정상 인식
// 0.01
new BigDecimal("0.01");

// 위와 동일한 결과, double#toString을 이용하여 문자열로 초기화
// 0.01
BigDecimal.valueOf(0.01);
```



## BigDecimal 비교 연산

```java
BigDecimal a = new BigDecimal("2.01");
BigDecimal b = new BigDecimal("2.010");

// 객체의 레퍼런스 주소에 대한 비교 연산자로 무의식적으로 값의 비교를 위해 사용하면 오동작
// false
a == b;

// 값의 비교를 위해 사용, 소수점 맨 끝의 0까지 완전히 값이 동일해야 true 반환
// false
a.equals(b);

// 값의 비교를 위해 사용, 소수점 맨 끝의 0을 무시하고 값이 동일하면 0, 적으면 -1, 많으면 1을 반환
// 0
a.compareTo(b);
```



## BigDecimal 사칙 연산

```java
BigDecimal a = new BigDecimal("10");
BigDecimal b = new BigDecimal("3");

// 더하기
// 13
a.add(b);

// 빼기
// 7
a.subtract(b);

// 곱하기
// 30
a.multiply(b);

// 나누기
// 3.333333...
// java.lang.ArithmeticException: Non-terminating decimal expansion; no exact representable decimal result.
a.divide(b);

// 나누기
// 3.333
a.divide(b, 3, RoundingMode.HALF_EVEN);

// 나누기 후 나머지
// 전체 자리수를 34개로 제한
// 1
a.remainder(b, MathContext.DECIMAL128);

// 절대값
// 3
new BigDecimal("-3").abs();

// 두 수 중 최소값
// 3
a.min(b);

// 두 수 중 최대값
// 10
a.max(b);
```



## BigDecimal 소수점 처리

> `RoundingMode.HALF_EVEN`은 **Java**의 기본 반올림 정책으로 금융권에서 사용하는 **Bankers Rounding**와 동일한 알고리즘, 금융권에서는 시스템 개발시 혼란을 막기 위해 요구사항에 반올림 정책을 명확히 명시하여 개발

```java
// 소수점 이하를 절사한다.
// 1
new BigDecimal("1.1234567890").setScale(0, RoundingMode.FLOOR);

// 소수점 이하를 절사하고 1을 증가시킨다.
// 2
new BigDecimal("1.1234567890").setScale(0, RoundingMode.CEILING);
// 음수에서는 소수점 이하만 절사한다.
// -1
new BigDecimal("-1.1234567890").setScale(0, RoundingMode.CEILING);

// 소수점 자리수에서 오른쪽의 0 부분을 제거한 값을 반환한다.
// 0.9999
new BigDecimal("0.99990").stripTrailingZeros();

// 소수점 자리수를 재정의한다.
// 원래 소수점 자리수보다 작은 자리수의 소수점을 설정하면 예외가 발생한다.
// java.lang.ArithmeticException: Rounding necessary
new BigDecimal("0.1234").setScale(3);

// 반올림 정책을 명시하면 예외가 발생하지 않는다.
// 0.123
new BigDecimal("0.1234").setScale(3, RoundingMode.HALF_EVEN);

// 소수점을 남기지 않고 반올림한다.
// 0
new BigDecimal("0.1234").setScale(0, RoundingMode.HALF_EVEN);
// 1
new BigDecimal("0.9876").setScale(0, RoundingMode.HALF_EVEN);
```



## BigDecimal 나누기 처리

```java
BigDecimal b10 = new BigDecimal("10");
BigDecimal b3 = new BigDecimal("3");

// 나누기 결과가 무한으로 떨어지면 예외 발생
// java.lang.ArithmeticException: Non-terminating decimal expansion; no exact representable decimal result.
b10.divide(b3);

// 반올림 정책을 명시하면 예외가 발생하지 않음
// 3
b10.divide(b3, RoundingMode.HALF_EVEN);

// 반올림 자리값을 명시
// 3.333333
b10.divide(b3, 6, RoundingMode.HALF_EVEN);

// 3.333333333
b10.divide(b3, 9, RoundingMode.HALF_EVEN);

// 전체 자리수를 7개로 제한하고 HALF_EVEN 반올림을 적용한다.
// 3.333333
b10.divide(b3, MathContext.DECIMAL32);

// 전체 자리수를 16개로 제한하고 HALF_EVEN 반올림을 적용한다.
// 3.333333333333333
b10.divide(b3, MathContext.DECIMAL64);

// 전체 자리수를 34개로 제한하고 HALF_EVEN 반올림을 적용한다.
// 3.333333333333333333333333333333333
b10.divide(b3, MathContext.DECIMAL128);

// 전체 자리수를 제한하지 않는다.
// java.lang.ArithmeticException: Non-terminating decimal expansion; no exact representable decimal result. 예외가 발생한다.
b10.divide(b3, MathContext.UNLIMITED);
```



## BigDecimal 문자열 변환 출력

> `.setScale()`을 사용하여 소수점 자리수를 제한하면 원본의 소수점 값은 상실해 버린다. 문자열로 출력하는 것이 목적이라면 `NumberFormat` 클래스를 사용하는 것이 적합

```java
NumberFormat format = NumberFormat.getInstance();
format.setMaximumFractionDigits(6);
format.setRoundingMode(RoundingMode.HALF_EVEN);
// 0.123457
format.format(new BigDecimal("0.1234567890"));
```



참조 : [지단로보트 티스토리](https://jsonobject.tistory.com/466)

