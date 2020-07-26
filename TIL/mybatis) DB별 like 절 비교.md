# mybatis) DB별 like 절 비교

### mybatis / ibatis  => #{ 키} / #키#



#### ORACLE LIKE

```sql
WHERE 컬럼명 LIKE '%'|| #{검색어} ||'%'
```





#### MySQL LIKE

```sql
WHERE 컬럼명 LIKE CONCAT('%', #{검색어}, '%')
```



#### MSSQL

```sql
WHERE 컬럼명 LIKE '%'+ #{검색어} +'%'
```





##### ++ 여러 조건검색

```sql
WHERE 컬럼명1 LIKE CONCAT('%', #{검색어}, '%') OR 컬럼명2 LIKE CONCAT('%', #{검색어}, '%') OR 컬럼명3 LIKE CONCAT('%', #{검색어}, '%')
```

