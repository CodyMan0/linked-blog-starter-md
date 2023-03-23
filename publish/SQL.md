# What is SQL
- 데이터 베이스안에 있는 데이터를 조회 수정 삭제 생성을 용도로 사용하는 것이 SQL문 

```jsx
SELECT * FROM Customers;
```
Customers 테이블 안에 있는 필드를 가지고 오겠다라는 의미 




## 문법
### SELECT 문
1. select : 조회 할때 

2.  만약 두가지 이상의 테이블에서 연관된 데이터를 찾아들어가서 가지고 오는 방식은 join이라는 함수를 쓴다는데? 
3. WHERE : 어떤 조건을 만족하는 것을 가지고 오라는 조건
4. FROM 은 가져올 테이블 정의
5. as 는 새로운 이름을 지어줄때 
6. 중복없이 데이터를 가져오고 싶을때쓰는 것이 SQL DISTINCT()

### INSERT 문 
1. INSERT INTO
2. VALUES value를 넣는 것

### UPDATE 문
```SQL
UPDATE Customers
SET Address = "강남구", City = "서울 특별기"
WHERE CustomerID = 92;
```
데이터를 수정할때는 UPDATE 문
set는 바꿀 필드와 값을 적어주고
WHERE은 조건 

### DELETE 문

 DELETE 문DELETE FROM Customers WHERE CustomerId=91;


## 중요한 것
1. 테이블은 각각 분리돼서 데이터베이스를 설계해야하고 그 흩어진 데이터에서 데이터를 조회할때는 SELECT를 쓰고 FROM에서 가져올 테이블 정의하고 WHERE 절에서 데이블 간에 연결 고리(키 값)들을 AND 조건으로 연결을 해줘야만 정확히 원하는 키값을 찾아 데이터를 가져온다는 것. 

2. 여러 테이블에서 원하는 자료를 SELECT 하는 방법을 배웠다.


### 참고 자료
- W3C 사이트 https://www.w3schools.com/sql/trysql.asp?filename=trysql_select_all


### 연결자료
[[NO-SQL]]
