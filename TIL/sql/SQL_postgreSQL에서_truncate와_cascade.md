# SQL) postgreSQL 에서 truncate와 cascade

```sql
-- truncate table은 롤백없이 데이터를 모두 지워버리고
-- delete 는 롤백가능하며 한 행씩 삭제
-- 테이블에 자동적으로 시퀀스 (자동증가 값)를 재시작하며 테이블 정보를 모두 삭제
truncate table 테이블 restart identity 

-- restart 와는 달리 테이블 시퀀스 값은 리셋하지 않고 데이터만 모두 삭제한다.
truncate table 테이블 continue Identity

-- 테이블 의 데이터를 모두 삭제하면 만약 테이블에 연결된 데이터들이 있다면
-- 해당 테이블의 데이터도 모두 삭제한다. (외래키로 연결된 데이터들)
truncate table 테이블 cascade

-- 테이블에 연결된 데이터가 하나라도 있다면 데이터를 삭제하지 않는다. 
-- casecade와 반대 개념 
truncate table 테이블 restrict

```





