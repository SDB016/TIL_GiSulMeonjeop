# 💡 관계형 데이터베이스의 특징  


# 💡 무결성 제약조건이란 무엇인가?    
데이터베이스의 일관성을 보장하기 위해        
**일관된 데이터베이스 상태를 정의하는 규칙**들을 묵시적으로 또는 명시적으로 정의하는 것     
   
## 개체 무결성 
> 기본키는 null이 될 수 없다.    
   
개체 무결성 제약조건은 기본키를 구성하는 모든 속성은 널 값을 가지면 안된다는 규칙이다.   
기본키는 릴레이션에 포함되는 튜플을 유일하도록 식별해주는 키로서,    
기본키를 구성하는 속성 전체나 일부가 널 값이 되면 튜플의 유일성을 판단할 수 없기 때문에 본질을 상실하게 된다.    
   
## 참조 무결성
> 외래키는 참조할 수 없는 값을 가질 수 없음    
                  
참조 무결성 제약조건은 외래키는 참조할 수 없는 값을 가질 수 없다는 규칙이다.      
외래키는 다른 릴레이션의 기본키를 참조하는 속성이고 릴레이션 간의 관계를 표현하는 역할을 한다.           
그런 외래키가 자신이 참조하는 릴레이션의 기본키와 상관없는 값을 가지게 되면      
두 릴레이션을 연관시킬 수 없으므로 외래키 본래의 의미가 없어진다는 문제점이 발생한다.           
        
## 도메인 무결성        
> 특정 속성값은 그 속성이 정의된 도메인에 속한 값이어야 한다.            
      
도메인 무결성은 데이터 베이스에 삽입되는 데이터들에 **제약 조건**을 의미합니다.             
각각의 속성은 `숫자, 문자 등의 도메인을 가지면 해당 도메인에 맞는 데이터를 삽입해야 한다.`      
그 뿐만 아니라 삽입되는 데이터를 제한하거나, 삽입되지 않을 경우 기본값, null 제한 등의 기능을 제공한다.  

## 키 무결성
> 릴레이션에는 최소한 하나의 키가 존재해야 함    
  
참고로 꼭 PK일 필요는 없다.     
애초에 DB에서는 Key가 없는 테이블을 작성할 수 있다.     
     
## null 무결성   
> 특정 속성은 null 값을 가질 수 없음    
             
null 무결성은 특정 속성값에는 null 값을 가질 수 없다는 규칙이다.     
기본적으로 속성값으로 null 값을 가질 수 있는데 만약 "유저 아이디"처럼 중요한 정보에는     
스키마를 정의할 때 해당 속성을 null 데이터가 올 수 없음을 미리 정의할 수 이다.      
   
## 고유 무결성
> 특정 속성값은 서로 달라야 함    
     
고유 무결성은 특정 속성에 삽입되는 데이터는 고유한 값을 가져야 한다는 규칙이다.      
이말은 즉, 각 튜플에서 하나의 속성값은 중복된 값이 없는 각각 서로 다른 값을 가져야 한다는 의미이다.       
예를 들어 이름, 나이, 사는 곳과 같은 속성은 튜프들이 서로 같은 값을 가질 수 있지만       
고객 아이디의 경우 각 튜플을 서로 다른 값을 가져야 한다.  

# 💡 View란 무엇인가?    
**Viwe :**    
본래 데이터베이스 객체로 등록할 수 없는 SELECT 명령을,    
객체로서 이름을 붙여 관리할 수 있도록 정의한 것           

뷰는 테이블처럼 취급할 수 있지만 '실체가 존재하지 않는다'라는 의미로 **'가상테이블'** 이라 불리기도 한다.   
뷰는 테이블처럼 데이터를 쓰거나 지울 수 있는 저장공간을 가지지 않는다.(물론 예외적인 방법은 있다.)  
이 때문에 테이블처럼 취급할 수 있다고 해도 SELECT 명령에서만 사용 하는 것을 권장한다.   
   
## 뷰의 장점      
**보안에 도움이 된다.**      
개인정보가 들어있는 테이블이 있다고 가정시    
이를 다름사람에게 권한을 부여하면 수정/삭제 등 데이터가 변경될 가능성   
개인정보 데이터를 조회함으로써 개인정보를 유출할 수 있기 때문에    
데이터 테이블 대신에 뷰에만 접근 권한을 주어 이러한 문제를 쉽게 해결한다.   
      
**복잡한 쿼리를 단순화 시켜 줄 수 있다.**  
코드가 긴 SELECT 쿼리가 있을시 이를 처음 작성하는 것은 문제가 없지만  
두번, 세번 즉 여러번 사용할 경우 코드 작성에대한 시간 소비가 많아 질 것이다.    
    
이렇듯 자주 사용하는 SELECT 쿼리문을 뷰로 만들어서    
재사용시 처음부터 다시 코드를 작성할 필요 없이 해당 뷰를 호출하면 된다.   
(WHERE 절 같은 추가 쿼리문도 뷰에 붙여서 사용하면 된다.)     

## 뷰의 약점
뷰는 데이터베이스 객체로서 저장장치에 저장된다.
하지만 테이블과 달리 대용량의 저장공간을 필요로 하지 않는다.
이유는 테이블을 저장하는 것이 아닌 명령어를 저장하는 것이기 때문이다.
다만 저장공간을 소비하지 않는 대신 CPU 자원을 사용한다.
이런 명령어들은 계산능력을 필요로 하기에 컴퓨터의 CPU를 사용하기 때문이다.
        
### 머티리얼라이즈드 뷰      
뷰의 근원이 되는 테이블 안에 보관하는 **데이터 양이 많은 경우,**    
또는 집계처리를 하는 경우에 뷰가 사용된다면 **처리속도가 많이 떨어진다.**   
또한 **뷰를 중첩해서 사용하는 경우에도 처리 속도가 떨어지기 쉽다.**   
        
이러한 문제점을 해결하기 위해 사용하는 것이 `머티리얼 라이즈드 뷰`이다.
일반적으로 뷰는 데이터를 일시적으로 저장했다가 쿼리가 실행 종료될 때 함께 삭제된다.
       
**머티리얼 라이즈드 뷰는 데이터를 `테이블처럼 저장장치에 저장`해두고 사용한다.**
머티리얼 라이즈드 뷰는 처음 참조되었을 때 데이터를 저장해둔다.  
이후 다시 참조할 때 **이전에 저장해 두었던 데이터를 그대로 사용한다.**  
다만 뷰에 지정된 테이블의 데이터가 변경된 경우에는 SELECT 명령을 재실행하여 데이터를 다시 저장해야 한다.
   
일종의 캐시 기능을 적용한 뷰   
즉, 뷰에 지정된 테이블의 데이터가 자주 변경되지 않는 경우라면 머티리얼라이즈드 뷰를 사용하자.
단 MySQL에서는 사용할 수 없다. Oracle과DB2에서만 사용할 수 있다.     
      
### 함수 테이블 - 이부분은 모르겠네요  
뷰를 구성하는 SELECT 명령은 단독으로 실행할 수 있어야 한다.
즉, 상관 서브 쿼리처럼, 부모 쿼리와 어떤 식으로든 연관된 서브쿼리의 경우에는 뷰의 SELECT 명령으로 사용할 수 없다.
대신 이 같은 뷰의 약점을 함수 테이블을 사용하여 회피할 수 있다.    
        
함수 테이블은 테이블을 결괏값으로 반환해주는 사용자 정의 함수이다.
함수에는 인수를 지정할 수 있기 때문에 인수의 값에 따라 WHERE 조건을 붙여 결괏값을 바꿀 수 있다.
그에 따라 상관 서브쿼리처럼 동작할 수 있다.   


# 💡 SQL과 NoSQL의 차이점에 대해 설명하시오.
## SQL      
SQL은 **`구조화 된 쿼리 언어 (Structured Query Language)`** 의 약자이다.      
그러므로 데이터베이스 자체를 나타내는 것이 아니라, 특정 유형의 데이터베이스와 상호 작용하는 데 사용 하는 쿼리 언어다.     
SQL을 사용하면 관계형 데이터베이스 관리 시스템(RDBMS)에서 데이터를 저장, 수정, 삭제 및 검색 할 수 있다.
     
이러한 관계형 데이터베이스에는 두 가지 주요 특징이 있다.      
* 데이터는 정해진(엄격한) 데이터 스키마 (= structure)를 따라 데이터베이스 테이블에 저장됩니다.   
* 데이터는 관계를 통해서 연결된 여러개의 테이블에 분산됩니다.      
   
**엄격한 스키마**   
데이터는 테이블(table)에 레코드(record)로 저장되며, 각 테이블에는 명확하게 정의된 구조(structure)가 있다. 
즉, 이를 다르게 풀어서 설명하자면 **스키마를 준수하지 않는 데이터는 레코드에 추가할 수 없다.**          
 
구조는 필드의 이름과 데이터의 유형(타입이나 제약조건)으로 정의, 도메인이라고보 부르기도 한다.       
다시 한번 말하지만, 관계형 db에서는 스키마를 준수하지 않는 레코드는 추가할 수 없다     
     
**관계**      
SQL 기반의 데이터 베이스의 또 다른 중요한 부분은 `관계`다.  
데이터들을 **여러개의 테이블에 나누어서, 데이터들의 중복을 피할 수 있다.**      
각각의 정보들을 테이블로 만들면 다른 테이블에 저장되지 않은 데이터 만을 가지고 있게 된다. (중복된 데이터가 없습니다.)    
이런 명확한 구조의 장점은 하나의 테이블에서 중복없이 하나의 데이터만을 관리하기 때문에,    
다른 테이블에서 부정확한 데이터를 다룰 위험이 없습니다.      
     
## NoSQL  



# 💡 Select 쿼리 실행 순서    
![select 절](https://user-images.githubusercontent.com/50267433/116062492-e9b6cb00-a6be-11eb-848d-4537bcce0bbb.png)    
  
```sql
 FROM - WHERE - GROUP BY - HAVING - SELECT - ORDER BY
```  
```sql  
 FROM - ON - JOIN - WHERE - GROUP BY - HAVING - SELECT - DISTINCT - ORDERBY - TOP    
```     
     
**쿼리 실행 순서는 왜 중요할까? 🤔**   
쿼리가 처리되고 어떻게 쿼리문을 작성하느냐에 따라 퍼포먼스의 차이가 발생한다.         
예를 들어, WHERE 절에 있는 내용을 HAVING절에서 사용할 수 있지만    
HAVING절에서 일반 조건들을 다루면 쿼리 실행 순서에 의해 퍼포먼스가 많이 떨어지게 된다.    
   
[매우 좋은 사이트](https://velog.io/@ha0kim/SQL)      
   
1. ALIAS 사용   
2. Oracle의 경우 Rownum

# 💡 PK와 FK 설명해주세요.
**PK**
* 테이블을 생성할 때 PK를 정의한다.
* PK는 각 행을고유하게 식별하는 역할을 담당한다.
* 테이블당 하나만 정의 가능하다.
* 지정된 컬럼에는 중복된 값이나 NULL값이 입력될 수 없다.
* NOT NULL + UNIQUE(UK)를 한 것과 같은 기능을 한다.
* PK로 지정 가능한 컬럼이 여러 개 있을 때는 검색에 많이 사용되고 간단하고 짧은 컬럼을 지정한다.
* 주 식별자, 주키 등으로 불린다.
* 고유 인덱스(Unique index)가 자동으로 생성된다.
       
**FK**     
* 테이블을 생성할 때 FK를 정의한다.        
* FK가 정의된 테이블이 자식 테이블이다.      
* 참조되는 테이블을 부모 테이블이라고 한다.    
* 부모 테이블은 미리 생성되어 있어야 한다.     
* 부모 테이블의 참조되는 컬럼에 존재하는 값만을 입력 할 수 있다.   
* 부모 테이블은 FK로 인해 삭제가 불가능하다.  
* 참조되는 컬럼은 PK이거나 UK(Unique key)만 가능하다.   
* 외부키, 참조키, 외부 식별자 등으로 불린다.   

# 💡 서브쿼리가 뭐에요? 
> 출처: [기본기를 쌓는 정아마추어 코딩블로그](https://jeong-pro.tistory.com/40 )
   
하나의 SQL 문에 포함되어 있는 또 다른 SQL 문을 말한다.       
쿼리문 관점에서 말하면 `SELECT 문` 안에 또다시 `SELECT문`이 있는 쿼리문이다.   
        
서브쿼리는 위치에 따라 명칭이 다르다.       
`FROM`절에 사용하는 `인라인 뷰(Inline view)`,        
`SELECT`문에 사용하는 `스칼라 서브쿼리(Scala Subquery)`,        
일반적으로 `WHERE`절에 사용하는 것을 `서브쿼리(Subquery)`라고 한다.        
        
## 단일 행 서브쿼리
```sql
SELECT PLAYER_NAME 선수명, POSITION 포지션, BACK_NO 백넘버
FROM PLAYER
WHERE TEAM_ID = (SELECT TEAM_ID
                 FROM PLAYER
                 WHERE PLAYER_NAME = '김남일')
ORDER BY PLAYER_NAME;
// 조금 억지로 만듦.
// 김남일 선수의 소속팀을 알아냄. 만약 김남일 선수가 동명이인으로 두명이상이 있다면 에러남
 
SELECT PLAYER_NAME 선수명, POSITION 포지션, BACK_NO 백넘버
FROM PLAYER
WHERE HEIGHT <= (SELECT AVG(HEIGHT)
                 FROM PLAYER)
ORDER BY PLAYER_NAME;
// 평균키를 알아내는 서브쿼리와 그 결과로 평균키 이하인 선수를 출력
```

## 다중 행 서브쿼리
서브쿼리의 결과가 2건이상 반환될 수 있다면 '반드시' 다중행 비교연산자(IN, ALL, ANY, SOME)과 함께 사용해야한다.    
      
* **IN(서브쿼리) :**   
  서브쿼리의 결과에 존재하는 값과 동일한 조건의미    
* **비교연산자 ALL(서브쿼리) :** 
  비교연산자에 `>` 를 썼다면 ALL이 모든 값을 만족하는 조건이기 때문에     
  결과중에 가장 큰값보다 커야 만족한다는 뜻.    
* **비교연산자 ANY(서브쿼리) :**    
  비교연산자에 ">" 를 썼다면 ANY가 어떤 하나라도 맞는지 조건이기 때문에    
  결과중에 가장 작은값보다 크면 만족한다는 뜻. (= SOME)   
* **EXISTS(서브쿼리) :**   
  서브쿼리의 결과를 만족하는 값이 존재하는지 여부 확인 1건만 찾으면 더이상 검색 안함    
   
```sql
SELECT REGION_NAME 연고지명, TEAM_NAME 팀명, E_TEAM_NAME 영문팀명
FROM TEAM
WHERE TEAM_ID IN (SELECT TEAM_ID
                  FROM PLAYER
                  WHERE PLAYER_NAME = '정현수')
ORDER BY TEAM_NAME;
// 정현수 선수가 두명이상 일때 소속 팀, 연고지명, 영문팀명 출력
```

## 다중 컬럼 서브쿼리
- 서브쿼리 결과로 여러 개의 컬럼이 반환되어 메인쿼리 조건과 동시에 비교되는 것.
```sql
SELECT TEAM_ID 팀코드, PLAYER_NAME 선수명, POSITION 포지션, BACK_NO 백넘버, HEIGHT 키
FROM PLAYER
WHERE (TEAM_ID, HEIGHT) IN (SELECT TEAM_ID, MIN(HEIGHT)
                            FROM PLAYER
                            GROUP BY TEAM_ID)
ORDER BY TEAM_ID, PLAYER_NAME;
// 소속팀별 키가 가장 작은 사람들의 정보를 출력.
// 같은 팀에서 여러명의 선수가 반환될 수 있음. 키가 같은 경우.
```
## 연관 서브쿼리 (Correlated Subquery)
```sql 
SELECT T.TEAM_NAME 팀명, M.PLAYER_NAME 선수명, M.POSITION 포지션, M.BACK_NO 백넘버, M.HEIGHT 키
FROM PLAYER M , TEAM T
WHERE M.TEAM_ID = T.TEAM_ID
AND M.HEIGHT < (SELECT AVG(S.HEIGHT)
                FROM PLAYER S
                WHERE S.TEAM_ID = M.TEAM_ID
                AND S.HEIGHT IS NOT NULL
                GROUP BY S.TEAM_ID)
ORDER BY 선수명;
// 선수 자신이 속한 팀의 평균키보다 작은 선수들의 정보를 출력하는 SQL문
SELECT STARDIUM_ID ID, STARDIUM_NAME 경기장명
FROM STARDIUM A
WHERE EXISTS (SELECT 1
              FROM SCHEDULE X
              WHERE X.STARDIUM_ID = A.STARDIUM_ID
              AND X.SCHE_DATE BETWEEN '20120501' AND '20120502')
// 20120501 과 20120502 사이의 날짜에 경기가 있는 경기장 조회
``` 
 
## SELECT 절에 서브쿼리 (=스칼라쿼리 : 한 행 한 컬럼만 반환하는 쿼리)
```sql
SELECT PLAYER_NAME 선수명, HEIGHT 키, ROUND( (SELECT AVG(HEIGHT)
                                             FROM PLAYER X
                                             WHERE X.TEAM_ID = P.TEAM_ID),3) 팀평균키
FROM PLAYER P
 
## FROM 절에 서브쿼리
SELECT T.TEAM_NAME 팀명, P.PLAYER_NAME 선수명, P.BACK_NO 백넘버
FROM (SELECT TEAM_ID, PLAYER_NAME, BACK_NO
      FROM PLAYER
      WHERE POSITION = 'MF') P,
      TEAM T
WHERE P.TEAM_ID = T.TEAM_ID
ORDER BY 선수명;
// 서브쿼리의 결과가 마치 동적으로 생성된 테이블처럼 사용
// 서브쿼리의 컬럼은 메인에서 사용할 수 없다. 하지만 이건 인라인뷰이기 때문에 사용가능
``` 
## TOP-N 쿼리
인라인 뷰에서는 ORDER BY절이 불가하다. 따라서 인라인 뷰에서 먼저 정렬하고 정렬된 결과에서 일부데이터를 추출하는 것이 TOP-N쿼리
TOP-N 쿼리를 수행하기 위해서는 ROWNUM이라는 연산자를 통해 건수를 제약할 수 있다.
```sql 
SELECT PLAYER_NAME 선수명, POSITION 포지션, BACK_NO 백넘버, HEIGHT ㅣ
FROM (SELECT PLAYER_NAME, POSITION, BACK_NO, HEIGHT
      FROM PLAYER
      WHERE HEIGHT IS NOT NULL
      ORDER BY HEIGHT DESC)
WHERE ROWNUM <= 5;
// 인라인 뷰에서 선수의 키를 내림차순으로 정렬한 후 메인쿼리에서 ROWNUM을 통해 5명만 추출.
// 즉, 키가 큰순서로 상위 5명 뽑음
``` 
## HAVING 절에 서브쿼리
```sql
SELECT P.TEAM_ID 팀코드, T.TEAM_NAME 팀명, AVG(P.HEIGHT) 평균키
FROM PLAYER P , TEAM T
WHERE P.TEAM_ID, T.TEAM_ID
GROUP BY P.TEAM_ID, T.TEAM_NAME
HAVING AVG(P.HEIGHT) < (SELECT AVG(HEIGHT)
                        FROM PLAYER
                        WHERE TEAM_ID = 'K02');
``` 
## UPDATE SET 절 서브쿼리
```sql
UPDATE TEAM A
SET A.E_TEAM_NAME = (SELECT X.STARDIUM_NAME
                     FROM STARDIUM X
                     WHERE X.STARDIUM_ID = A.STARDIUM_ID);
``` 
## INSERT VALUES 절에 서브쿼리
```sql
INSERT INTO PLAYER(PLAYER_ID, PLAYER_NAME, TEAM_ID)
VALUES( (SELECT TO_CAHR(MAX(TO_NUMBER(PLAYER_ID))+1) FROM PLAYER), '홍길동','K06');
```
## 뷰
테이블은 실제 데이터를 가지고 있는 반면, 뷰는 실제 데이터가 없음
테이블 구조가 변경되어도 뷰를 사용하는 응용프로그램은 변경하지 않아도 됨.
```sql 
CREATE VIEW V_PLAYER_TEAM AS
SELECT P.PLAYER_NAME ,P.POSITION, P.BACK_NO, P.TEAM_ID, T.TEAM_NAME
FROM PLAYER P , TEAM T
WHERE P.TEAM_ID = T.TEAM_ID;
```
# 💡 서브쿼리의 성능은 어때요?
* MySQL 5.5 까지는 서브쿼리 최적화가 최악이라 웬만하면 Join으로 전환하자
  * 메인테이블의 row 수 만큼 서브 쿼리를 수행한다
  * MySQL 5.6 에서 서브 쿼리가 대폭 최적화 되었다.
  * 다만 최적화가 적용 안되는 조건들이 다수 존재한다
* 버전/조건 관계 없이 좋은 성능을 내려면 최대한 Join을 이용하자
  * Join을 사용하기가 너무 어렵다면 Subquery는 사용하되, MySQL 5.5 이하라면 절대 사용하지 않는다. 
  * 차라리 쿼리를 나눠서 2번 실행 (메인쿼리/서브쿼리)하고 애플리케이션에서 조립하는게 낫다.

# 💡 %LIKE%와 elasticsearch의 차이점을 설명해주세요. 
   
1. 관계형 데이터베이스는 단순 텍스트매칭에 대한 검색만을 제공
2. MySQL 최신 버전에서 n-gram 기반의 Full-text 검색을 지원하지만, 한글 검색의 경우에 아직 많이 빈약한 감이 있습니다.
3. 텍스트를 여러 단어로 변형하거나 텍스트의 특질을 이용한 동의어나 유의어를 활용한 검색이 가능
4. 비정형 데이터의 색인과 검색이 가능
5. 형태소 분석을 통한 자연어 처리가 가능
6. 역색인 지원으로 매우 빠른 검색이 가능

# 이건 잠시 저장
SOAP방식과 REST방식의 차이점은?  
