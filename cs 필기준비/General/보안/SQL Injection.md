# SQL Injection
    
임의의 SQL 문을 주입하고 실행되게 하여 데이터베이스가 비정상적인 동작을 하도록 조작하는 행위다.       
공격이 비교적 쉬운 편이지만, DB에 있는 실제 데이터를 변경하거나 탈취하는등 큰 피해를 줄 수 있다.    

## Error based SQL Injection

논리적 에러를 이용한 SQL Injection 으로 가장 대중적인 공격 기법이다.     
    
```sql 
OR 1=1 -- 
```         
* `OR 1=1`를 통해 WHERE 절을 모두 참으로 만든다.      
* `--` 를 넣어줌으로 뒤의 구문을 모두 주석 처리한다.        

## Union based SQL Injection
     
Union 키워드를 사용하여 원하는 쿼리문을 실행할 수 있게 하는 공격 기법이다  .   
단, Union Injection을 성공하기 위해서는 두 가지의 조건이 있다.     

1. Union 하는 두 테이블의 컬럼 수가 같아야 한다
2. 데이터 형이 같아야 합니다.    

# 방지 

## PreparedStatement
 
## JPA는?    

JPA는 
JPA는 내부 구현이 PreparedStatement 로 되어있다.   
