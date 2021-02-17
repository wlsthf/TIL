# SQL) 쿼리 속도 향상

1. ### SELECT 시에는 꼭 필요한 칼럼만 불러온다.

   - ###### 필드 값이 많을 수록 DB에 부담이 된다.

   

2. ### 조건 부여 시 별도 연산을 걸지 않는 것이 좋다.

   ```SQL
   -- WHERE FLOOR(value/2) = 2 
   
   WHERE value BETWEEN 4 AND 5 
   ```

   

3. ### LIKE 사용시 %는 문자열 앞부분에는 배치하지 않는 것이 좋다.

   ##### "...%"  검색을 해라

   ###### Comedy와 Romantic Comedy를 추출 할 경우 ( 속도가 느린 순서)

   ```sql
   WHERE value LIKE "%Comedy"  
   
   WHERE value = "Romantic Comedy" OR value = "Comedy"
   
   WHERE value IN ("Romantic Comedy", "Comedy") 
   
   WHERE value LIKE "Romantic%" OR value LIKE "Comed%"
   ```

   

4. ### 중복값 제거 ( SELECT DISTINCT, UNION DISTINCT)연산은 최대한 사용하지 않는 것이 좋다.

   - ###### EXISTS를 대체로 사용

     

5. ### 같은 내용의 조건이라면, GROUP BY 연산 시 HAVING 절 보다는 WHERE 절이 좋다.

   - ######  WHERE 절이 HAVING절보다 먼저 실행된다. WHERE절로 미리 데이터의 크기를 줄이고 탐색하자.

     

6. ### 3개 이상의 테이블을 INNER JOIN 할 때는, 크기가 가장 큰 테이블을 FROM 절에 배치하고, INNER JOIN 절에는 남은 테이블을 작은 순서대로 배치하는 것이 좋다.

   - ###### 많고 복잡할 수록 잘 생각해서 짜야한다.

     

7. ### 자주 사용하는 데이터의 형식에 대해서는 미리 전처리된 테이블을 따로 보관/관리 하는 것도 좋다.

   - ###### 데이터를 분석할때 많이 사용되는 편..

     

8. ### ORDER BY 는 연산 중간에 사용하지 않는 것이 좋다.

9. ### LIMIT를 활용하는 습관을 들이는 것이 좋다.





참조: [daniel님의 WATCHA](https://medium.com/watcha/%EC%BF%BC%EB%A6%AC-%EC%B5%9C%EC%A0%81%ED%99%94-%EC%B2%AB%EA%B1%B8%EC%9D%8C-%EB%B3%B4%EB%8B%A4-%EB%B9%A0%EB%A5%B8-%EC%BF%BC%EB%A6%AC%EB%A5%BC-%EC%9C%84%ED%95%9C-7%EA%B0%80%EC%A7%80-%EC%B2%B4%ED%81%AC-%EB%A6%AC%EC%8A%A4%ED%8A%B8-bafec9d2c073)