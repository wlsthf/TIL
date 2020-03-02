# SQL ) EXISTS, NOT EXISTS 

###### EXISTS : 서브 쿼리가 적어도 하나의 행을 돌려주면 TRUE가 된다.

###### NOT EXISTS : 서브 쿼리가 적어도 하나의 행을 돌려주지 않으면 TRUE가 된다.




--  myemp1 테이블에서 퇴사자가 존재하면 1’을 출력하시오

```sql
select 1 from dual
 where exists 
 	(
        select empno from myemp1
 		where outdate is not null
    );
```





--  EMP테이블에서 job중 ‘ORACLEJAVA’ 가 없으면 1을 출력하시오.

```sql
select 1 from dual
where not exists 
	( 
        select job from emp
		where job = 'ORACLEJAVA'
    );
```







[출처 : 오라클자바 커뮤니티 ](http://ojc.asia/bbs/board.php?bo_table=LecSQLnPlSql&wr_id=253) 

