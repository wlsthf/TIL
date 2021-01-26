# SQL) sql  에서 날짜 계산



```sql
-- mySQL
DATE_ADD(STR_TO_DATE('2020-09-14 03:00:00', '%Y-%m-%d %h:%i:%s') , INTERVAL -24 HOUR;
         
-- postgreSQL
to_char(to_timestamp('2020-09-14 03:00:00', 'yyyymmddhh24')::timestamp with time zone + '1 hour', 'yyyymmddhh24');
to_char(to_timestamp('2020-09-14 03:00:00', 'yyyymmddhh24')::timestamp with time zone - '2 months', 'yyyymmddhh24');
```

