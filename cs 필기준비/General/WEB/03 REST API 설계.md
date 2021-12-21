


   
# REST API 설계       
REST API는 다음과 같이 구성합니다.        
     
* 자원 : URI   
* 행위 : HTTP 메서드   
* 표현 : 리소스에 대한 표현 (HTTP Message Body)       
    
## URI 설계                  
### 명사를 사용해라   
```      
GET http://localhost:8080/api/books   
content-type: application/json
```   
동사를 표현할 때는 **HTTP 메서드인 GET, POST, PUT, DELETE 등으로 사용하면 된다.**     
그러나 간혹, 동사형을 사용할 수 있다.  
  
### 복수형을 사용해라         
복수형을 사용하면, 컬렉션 또한 명확하게 표현할 수 있어 확장성 측면에서 더 좋다.      

```js    
{
     books: [
          {
               book: ...
          },
          ...
     ]
}
```  
컬렉션으로 URI를 사용할 경우, 컬렉션을 한번 더 감싼 중첩 형식을 사용할 수 있다.         
`-embedded : []`를 외부 중첩 형식으로 도입한다고 해도 내부에 기존 컬레션 키 값이 유지된다.               
서버의 API 스펙이 변경되더라도 클라이언트는 따로 코드를 수정할 필요가 없다.             
  
### 슬래시 구분자(/)는 계층 관계를 나타내는 데 사용해라 

```
http://restapi.example.com/houses/apartments
http://restapi.example.com/animals/mammals/whales
```  
   
REST는 계층 구조를 표현하기에 적합한 아키텍처이다.  

### URI 마지막 문자로 슬래시(/)를 포함하지 않는다.
```
http://restapi.example.com/houses/apartments/ (X)
http://restapi.example.com/houses/apartments  (0)
```  
   
URI 경로의 마지막에는 슬래시(/)를 사용하는 것은 리소스 입력 여부에대한 혼돈을 줄 수 있다.     
그러므로 URI 경로의 마지막에는 슬래시(/)를 사용하지 않는다.    

### 하이픈(-)은 URI 가독성을 높이는데 사용  
    
URI를 쉽게 읽고 해석하기 위해, 불가피하게 긴 URI경로를 사용하게 된다면 하이픈을 사용해 가독성을 높일 수 있다.   
    
### 밑줄 (_)은 URI에 사용하지 않는다.        
      
글꼴에 따라 다르지만 밑줄은 보기 어렵거나 밑줄 때문에 문자가 가려지기도 한다.           
이런 문제를 피하기 위해 밑줄 대신 하이픈(-)을 사용하는 것이 좋다.  

### URI 경로에는 소문자가 적합하다.   
  
URI는 대소문자에 따라 리소스를 다르게 인식한다.         
     
### 파일 확장자는 URI에 포함시키지 않는다.

```
http://restapi.example.com/members/soccer/345/photo.jpg (X)
```
   
REST API에서는 메시지 바디 내용의 포맷을 나타내기 위한 파일 확장자를 URI 안에 포함시키지 않는다.     

### 리소스 간의 관계를 표현  

```
             /리소스명/리소스 ID/관계가 있는 다른 리소스명  
ex)    GET : /users/{userid}/devices (일반적으로 소유 ‘has’의 관계를 표현할 때)   
```   
REST 리소스 간에는 연관 관계가 있을 수 있고, 이런 경우 위와 같은 표현 방법을 사용한다.   
만약에 관계명이 복잡하다면 이를 서브 리소스에 명시적으로 표현하는 방법도 있다.    
 
```
GET /users/{userid}/likes/devices (관계명이 애매하거나 구체적 표현이 필요할 때)   
```  
예를 들어 사용자가 ‘좋아하는’ 디바이스 목록을 표현해야 할 경우 위와 은 형태로 사용될 수 있다.   
    
### 행위 설계             
          
REST API는 `명사+복수형`을 권장하기에 페이징을 처리하는 값을 추가로 제공할 수도 있다.         
쿼리 스트링으로 페이지, 크기, 정렬, 등의 파라미터를 지정할 수 있다.      

```
GET http://localhost:8080/api/books?page=0&size=10&sort=desc
content-type: application/json    
```    
page, size, sort 파라미터를 따로 지정하지 않으면 서버에서 기본으로 설정한 값으로 반환된다.      
 
