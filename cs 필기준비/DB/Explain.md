# MySQL 옵티마이저 구조 

![mysql-sql-executor-flow](https://user-images.githubusercontent.com/50267433/146498116-473b07ec-4ed5-44c9-90bc-6030e9aeccbc.png) 

**MySQL 옵티마이저**는 비용 기반으로, 어떤 실행 계획으로 쿼리를 실행했을 때 비용이 얼마나 발생하는지를 계산하여 비용이 가장 적은 것을 택한다.   
어디까지나 추정 값이므로 정확한 비용은 실행전까지 정확히 알 수 없다.  

MySQL 8.x 대에서 성능이 2~3배 향상되었다는 얘기도 있다.  

# Explain  
   
Explain은 MySQL 서버가 어떠한 쿼리를 실행할 것인가.        
즉, **실행 계획이 무엇인지 알고 싶을 때 사용하는 기본적인 명령어이다.**       

|id|select_type|table|partitions|type|possible_keys|key|key_len|ref|rows|filtered|Extra|
|-|------------|-----|----------|----|-------------|---|-------|---|----|--------|-----|
|‘1’|‘SIMPLE’|‘m’|NULL|‘range’|‘PRIMARY’|‘PRIMARY’|‘8’|NULL|‘3’|‘100.00’|‘Using where’|
|‘1’|‘SIMPLE’|‘o’|NULL|‘ref’|‘FKpktxw…’|‘FKpktxw…’|‘8’|‘sample.m.id’|‘90’|‘100.00’|NULL|
|‘1’|‘SIMPLE’|‘t’|NULL|‘eq_ref’|‘PRIMARY’|‘PRIMARY’|‘8’|‘sample.o.transaction_id’|‘1’|‘100.00’|NULL|

* table: 접근하고 있는 테이블에 대해 표시한다(alias로 보여줌)   
* id : select에 붙은 번호,   
* select_type : 대부분 SIMPLE 값이 출력되고, 서브쿼리나 UNION을 사용하면 바뀐다.   
* partitions : 파티셔닝 되어있는 경우에 사용된다.   
* type : 
*
**
