# MySQL 옵티마이저 구조 

![mysql-sql-executor-flow](https://user-images.githubusercontent.com/50267433/146498116-473b07ec-4ed5-44c9-90bc-6030e9aeccbc.png) 

1. 사용자로부터 요청된 SQL 문장을 잘게 쪼개서 MySQL 서버가 이해할 수 있는 수준으로 분리한다.
2. SQL의 파싱 정보(파스 트리)를 확인하면서 어떤 테이블부터 읽고 어떤 인덱스를 이용해 테이블을 읽을지 선택한다.
3. 두번째 단계에서 결정된 테이블의 읽기 순서나 선택된 인덱스를 이용해 스토리지 엔진으로부터 데이터를 가져온다.

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
* partitions : 파티셔닝 되어있는 경우에 사용된다.(없으면 null)      
* type : 접근 방식을 표현한다.   
    테이블에서 어떻게 행 데이터를 가져올 것인가, 대상 테이블로의 접근이 효율적일지 여부를 판단하는 아주 중요한 항목     
    * ALL : 전체 행 스캔, 테이블의 데이터 전체에 접근한다.   
    * index : 인덱스 스캔, 테이블의 특정 인덱스의 전체 엔트리에 접근한다.  
    * eq_ref : 
    * ref : 
    * fulltext: fulltext 인덱스를 사용한 검색 
    * 
* possible_keys : 
    * 이용 가능성이 있는 인덱스의 목록 
* key :
    * 이용 가능성이 있는 인덱스의 목록 중, 실제로 옵티마이저가 선택한 인덱스     
    * null 인 경우는, 행 데이터를 가져오기 위해 인덱스를 사용할 수 없다는 뜻이다.    
* key_len : 
    * 선택된 인덱스의 길의를 나타낸다(인덱스가 너무 긴 것도 비효율적이므로)   
* rows :
    * 해당 접근 방식을 사용해서 몇 행을 가져왔는가를 표시한다.   
    * 최초에 접근하는 테이블에 대해서 쿼리 전체에 의해 접근하는 행의 수
    * 그 이후에 테이블에 대헤서는 1행의 조인으로 평균 몇 행에 접근했는가를 표시한다.  
    *    


# Slow 쿼리 

