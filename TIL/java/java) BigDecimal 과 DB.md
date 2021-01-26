# java) BigDecimal 과 DB



## MySQL과 BigDecimal

> **MySQL** 또한 **Java**와 동일한 문제를 가지고 있다. **FLOAT**, **DOUBLE** 타입에 소수를 가진 수를 저장할 경우 앞서와 동일한 연산의 정확도 문제가 발생한다. 이를 해결하기 위해 **MySQL**은 **BigDecimal** 타입에 대응하는 `DECIMAL` 타입을 제공한다. 컬럼 선언 방법은 아래와 같다

```mysql
foo DECIMAL(5,2) DEFAULT 0.00 NOT NULL
```



## PostgreSQL

> **_numric** 형식의 컬럼은 **BigDecimal** 얻어진다. typeHandler를 사용해야한다.
>
> typeHandler정리 : https://github.com/NickKies/TIL/blob/master/TIL/mybatis)%20배열%20컬럼%20처리.md





## JPA에서 BigDecimal 처리

> - **JDBC**에서 **MySQL/MariaDB**의 `DECIMAL` 타입은 `ResultSet` 인터페이스의 `getBigDecimal()`, `getString()` 2개 메써드로 획득이 가능하다. [[관련 링크\]](https://www.cis.upenn.edu/~bcpierce/courses/629/jdkdocs/guide/jdbc/getstart/mapping.doc.html) **JPA** 또한 별도의 작업 없이 엔티티 필드에 **BigDecimal** 타입을 사용하여 처리하면 된다.
> - 만약, 데이터베이스 저장시 소수점 이하 자리수와 반올림 방법을 자동으로 처리되게 하고 싶다면 **JPA**가 제공하는 커스텀 컨버터를 제작하면 된다. 커스텀 컨버터 작성 예는 아래와 같다. **Kotlin**으로 작성하였다.

```java
// 소수점 이하 6자리에서 Bankers Rounding을 적용하여 BigDecimal 값을 생성한 후 데이터베이스에 저장하는 역할의 컨버터
class BigDecimalScale6WithBankersRoundingConverter : AttributeConverter<BigDecimal, String> {

    companion object {

        const val SCALE_SIX = 6
        val BANKERS_ROUNDING_MODE = RoundingMode.HALF_EVEN
    }

    override fun convertToDatabaseColumn(attribute: BigDecimal?): String? {

        return when (attribute?.scale()) {
            null -> null
            SCALE_SIX -> attribute.toString()
            else -> attribute.setScale(SCALE_SIX, BANKERS_ROUNDING_MODE).toString()
        }
    }

    override fun convertToEntityAttribute(dbData: String?): BigDecimal? {

        return when (dbData) {
            null -> null
            else -> BigDecimal(dbData)
        }
    }
}
```

커스텀 컨버터를 적용하는 예

```java
// DECIMAL(21,6) 타입에 대한 맵핑 상세 정의
// 숫자 범위는 -999999999999999.999999 ~ +999999999999999.999999
@Column(name = "foo", nullable = false, precision = 21, scale = 6)
@Digits(integer = 15, fraction = 6)
@Convert(converter = BigDecimalScale6WithBankersRoundingConverter::class)
var foo: BigDecimal? = BigDecimal.ZERO
```



## Spring Data MongoDB에서의 BigDecimal 처리

> - **Spring Data MongoDB**는 기본적으로 **BigDecimal** 타입의 필드를 **String** 타입으로 저장하고 읽어들인다. 문제는 **String** 타입의 필드는 도큐먼트 간의 정렬 및 연산시 의도하지 않은 결과를 초래할 수 있다. [[관련 링크\]](http://www.mytechtip.com/2018/01/sort-bigdecimal-mongodb-spring-data.html) 이러한 문제를 예방하려면 **String**이 아닌 **Decimal128**(2016-11-29 출시된 **MongoDB 3.4**부터 지원함에 유의) 타입으로 저장하도록 컨버터를 제작해야 한다. **MongoDB**의 경우 **JPA**와는 다르게 개별 필드 레벨로는 컨버터 생성이 불가능하고 별도의 통합된 `org.springframework.data.mongodb.core.convert.CustomConversions` 커스텀 빈을 작성해야 한다.
> - 첫번째 방법은 아래와 같이 개별 컨버터를 따로 만드는 것이다. 저장할 때와 불러올 때의 컨버터를 각각 따로 만들어야 한다.

```java
package com.jsonobject.example;

import java.math.BigDecimal;
import org.bson.types.Decimal128;
import org.springframework.core.convert.converter.Converter;

public class Decimal128ToBigDecimalConverter implements Converter<Decimal128, BigDecimal> {

    @Override
    public BigDecimal convert(Decimal128 source) {

        return source == null ? null : source.bigDecimalValue();
    }
}
```



```java
package com.jsonobject.example;

import java.math.BigDecimal;
import org.bson.types.Decimal128;
import org.springframework.core.convert.converter.Converter;

public class BigDecimalToDecimal128Converter implements Converter<BigDecimal, Decimal128> {

    @Override
    public Decimal128 convert(BigDecimal source) {

        return source == null ? null : new Decimal128(source);
    }
}
```

앞서 제작한 컨버트를 적용하여 컨버터 빈을 생성하면 첫번째 방법은 적용이 완료된다

```java
package com.jsonobject.example;

import java.util.Arrays;
import com.jsonobject.example.BigDecimalToDecimal128Converter;
import com.jsonobject.example.Decimal128ToBigDecimalConverter;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.data.mongodb.MongoDbFactory;
import org.springframework.data.mongodb.core.convert.CustomConversions;
import org.springframework.data.mongodb.core.convert.DbRefResolver;
import org.springframework.data.mongodb.core.convert.DefaultDbRefResolver;
import org.springframework.data.mongodb.core.convert.DefaultMongoTypeMapper;
import org.springframework.data.mongodb.core.convert.MappingMongoConverter;
import org.springframework.data.mongodb.core.mapping.MongoMappingContext;

@Configuration
public class MongoConfig {

    @Autowired
    private MongoDbFactory mongoFactory;

    @Autowired
    private MongoMappingContext mongoMappingContext;

    @Bean
    public MappingMongoConverter mongoConverter() {

        DbRefResolver dbRefResolver = new DefaultDbRefResolver(mongoFactory);
        MappingMongoConverter mongoConverter = new MappingMongoConverter(dbRefResolver, mongoMappingContext);
        mongoConverter.setTypeMapper(new DefaultMongoTypeMapper(null));
        mongoConverter.setCustomConversions(new CustomConversions(Arrays.asList(
            new BigDecimalToDecimal128Converter(),
            new Decimal128ToBigDecimalConverter()
        )));

        return mongoConverter;
    }
}
```

- 두번째 방법은 훨씬 간단하다. **CustomConversions** 빈만 생성하면 된다. 개별 컨버터를 제작할 필요도 없다.

```java
package com.jsonobject.example;

import java.math.BigDecimal;
import java.util.Arrays;
import org.bson.types.Decimal128;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.core.convert.converter.Converter;
import org.springframework.data.mongodb.core.convert.CustomConversions;

@Configuration
public class MongoConfig {

    @Bean
    CustomConversions customConversions() {

        Converter<Decimal128, BigDecimal> decimal128ToBigDecimal = new Converter<Decimal128, BigDecimal>() {
            @Override
            public BigDecimal convert(Decimal128 source) {

                return source == null ? null : source.bigDecimalValue();
            }
        };

        Converter<BigDecimal, Decimal128> bigDecimalToDecimal128 = new Converter<BigDecimal, Decimal128>() {
            @Override
            public Decimal128 convert(BigDecimal source) {

                return source == null ? null : new Decimal128(source);
            }
        };

        return new CustomConversions(Arrays.asList(decimal128ToBigDecimal, bigDecimalToDecimal128));
    }
}
```

