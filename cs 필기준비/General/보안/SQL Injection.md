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
## 입력 값에 대한 검증
  
요청을 처리하는 과정에서 쿼리문 존재 여부를 확인하고 이를 필터링한다.   

## PreparedStatement   
    
Prepared Statement 구문을 사용하게 되면,       
**사용자의 입력 값이 데이터베이스의 파라미터로 들어가기 전에DBMS가 미리 컴파일 하여 실행하지 않고 대기한다.**       
그 후 사용자의 입력 값을 아무 의미 없는 단순 문자열로 인식하게 하여 쿼리를 실행하지 못하게끔 한다.     

## Error Message 노출 금지

에러가 발생해도 어디가 문제인지와 같은 메시지를 노출시키지 않도록한다.  

# JDBC에서는?  
      
Statement 대신 **PreparedStatement를 사용하자.**       
쿼리를 수행하기 전에 이미 쿼리가 컴파일 되어 있으며,    
반복 수행의 경우 프리 컴파일된 쿼리를 통해 수행이 이루어져서 속도가 빠르며 SQL Injection 등의 문제도 보완해준다         
  
# MyBatis에서는?  

MyBatis에서는 `${}` 문법과 `#{}` 문법을 지원하고 있다.    
  
* `#{}` 문법 : Parameter Binding을 활용하여 여러 Escape를 통해 파라미터를 생성하고 parameter를 sql에 binding 하게 해준다.    
* `${}` 문법 : SQL 쿼리문에 직접 꽂기 때문에(Query String) 위와 같은 SQL Injection 공격이 가능해진다.   
  
# Spring Data JPA는?    
   
JPA는 내부적으로 Parameter Binding을 활용하고 있다고 공식적으로 이야기하고 있다.      
하지만, SQL 쿼리 스트링을 직접 짜서 entityManager에 전달한다던가의 JPA 활용은 다소 위험을 유발할 수 있다.       
