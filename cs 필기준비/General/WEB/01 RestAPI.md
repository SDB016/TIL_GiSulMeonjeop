# REST API  
     
* REST : 분산 하이퍼미디어 시스템(웹)을 위한 아키텍처 스타일     
* REST API : REST 아키텍처 스타일을 따르는 API     
* 아키텍처 스타일 : 제약 조건의 집합    
                 
REST API는 REST 제약 조건의 집합을 모두 지킨 API를 의미한다.               
하지만, 대부분의 개발자이 API가 REST 조건을 지키지 못했음에도 REST API라고 부르고 있으며                 
이에따라 REST의 창시자 Roy Fielding 은 다른 용어를 사용하기를 제시했다.          
  
**이로인해, 현재는 REST 구현 원칙을 제대로 지킨 API를 RESTful API라고 부르기 시작했다.**    
      
## REST 제약 조건    

* client-server
* stateless 
* cache 
* layer system
* code-on-demand(optional)    
* **uniform interface**  

### Client-Server 
   
* 기본 원칙은 관심사의 명확한 분리다.   
* 관심사의 명확한 분리가 선행되면 서버의 구성요소가 단순화되고 확장성이 향상되어 여러 플랫폼을 지원할 수 있다.            
   
### Stateless 
     
* 서버에 클라이언트의 상태 정보를 저장하지 않는다.                      
* 들어오는 요청만 처리하여 구현을 더 단순화된다.                 
* 단, **클라이언트의 모든 요청은 서버가 요청을 알아듣는데 필요한 모든 정보를 담고 있어야 한다.**           
      
### Cache     
  
* 클라이언트에게 보내는 응답을 캐시할 수 있어야 한다.       
* HTTP가 제공하는 캐시인 Cache-Control과 같은 기능들을 제공할 수 있어야 한다.      

### Layer System 

* 서버는 게이트웨이, 프록시, 로드 밸런싱, 공유 캐시등의 기능을 사용하여 확장성 있는 시스템을 구성할 수 있다.  
   
### Code On Demand

* 서버에서 코드를 보내면 클라이언트에서 바로 실행가능해야한다

### Uniform Interface  
  
* URI로 지정된 리소스에 균일하고 통일된 인터페이스를 제공한다.       
* 아키텍처를 단순하게 분리하여 단순하게 만들 수 있습니다.            
* 햔대 API 들을 REST API가 아니라고 말하는 가장 중요한 요소이다.       
   
# Uniform Inteface  

* URI로 지정된 리소스에 균일하고 통일된 인터페이스를 제공한다.       
* 아키텍처를 단순하게 분리하여 단순하게 만들 수 있습니다.            
* 햔대 API 들을 REST API가 아니라고 말하는 가장 중요한 요소이다.       
   
**필요성 - 독립적 진화를 제공해준다.**      
* 서버와 클라이언트가 각각 독립적으로 진화한다.       
* 서버의 기능이 변경되어도 클라이언트를 업데이트할 필요가 없다.      
* REST를 만들게 된 계기 : HOW DO IMPORVE HTTP WITHOUT BREAKING THE WEB   
    
**인터페이스 일관성**          
1. Identification of resources                  
2. Manipulation of resources through representations     
3. Self-descriptive messgae          
4. Hypermedia as the engine of application state(HATEOAS)  
        
## Identification of resources      

```
http://localhost:8080/resource/1
```

* 리소스를 통해서 자원을 식별할 수 있어야한다.    
* 웹 기반의 REST에서 리소스 접근을 주로 URI를 사용한다.            

## Manipulation of resources through representations     
  
```  
http://localhost:8080/resource/1

{
    id: 1,
    data: {
        name: 'wooji'
    }
}
```   
  
* 메시지나 메타 데이터를 가지고 충분한 정보를 전달할 수 있어야한다.           

            
## Self-descriptive messgae 
   
HTTP 메시지는 자신의 모든 요소에 대해서 완벽히 해석되어야한다.      
    
```
http://localhost:8080/resource/1

{
    id: 1,
    data: {
        name: 'wooji'
    }
}
```
* 목적지 Host가 빠져있다.         

```
http://localhost:8080/resource/1  
Host: localhost:8080     

{
    id: 1,
    data: {
        name: 'wooji'
    }
}
```   

* 어떤 문법으로 작성되었는지 모른다.   

```
http://localhost:8080/resource/1  
Host: localhost:8080     
Content-Type: application/json

{
    id: 1,
    data: {
        name: 'wooji'
    }
}
```  
* id, data, name이 무엇을 의미하는지 모른다.    

```
http://localhost:8080/resource/1  
Host: localhost:8080     
Content-Type: application/json-my-json

{
    id: 1,
    data: {
        name: 'wooji'
    }
}
```
* application/json-my-json 이라는 미디어타입을 IANA에 등록한다.       
* 등록하면서, id, data, name이 무엇인지 설명을 명세한다.             
* 사용자는 해당 명세서(문서)를 통해서 어떤 의미인지 이해할 수 있다.    

이로서 모든 요소에 대해서 설명이 가능해졌다.   

**IANA에 등록하는 것은 필수인가?**   
* 아니다. 하지만 아래와 같은 장점을 가지고 있다.   
* 누구나 쉽게 사용할 수 있다.   
* 이름 충돌을 피할 수 있다.    
* 등록이 별로 어렵지 않다.   
  
## Hypermedia as the engine of application state(HATEOAS)     
      
애플리케이션의 상태는 Hyperlink를 이용해 전이될 수 있어야한다.        

![image](https://user-images.githubusercontent.com/50267433/146884796-1ae90e1e-ade8-44f0-ad61-5120d1fd7e2a.png)  

상태가 전이된다는 하나의 행동에서 다른 행동으로 그 흐름이 이어질 수 있어야 한다는 뜻이다.   
즉, HTTP를 이용해서, 다음 페이지(상태)들로 동적으로 이동이 가능해야한다.   

```
HTTP/1.1 200 OK
Content-Type: text/html

<html>
<head></head>
<body><a href="/test">test</a></body>
</html>
```
* HTML 데이터는 `href`를 이용하여 다음 상태를 표현할 수 있다.   

```
HTTP/1.1 200 OK
Content-Type: text/html
Link: </article/1>; rel="previous"
      </article/3>; rel="next"
   
{
    "title": "The seconds article",
    "contents": "blah blah.."
}
```
* JSON은 Link 헤더를 이용해 표현할 수 있다.    
* 또는 JSON 데이터에 다음 링크를 남겨둘 수 있다.    


**HATEOAS 작업을 하면 얻게되는 이점**                   
* 클라이언트는 관련된 특정 동작에 따라 탐색할 만한 URI 값을 알 수 있다.                     
  URI는 resource 까지 포함하므로 더 명확하게 예측이 가능하다.                            
* 키 값이 변하지 않는 한 URI가 변경되더라도 동적으로 사용할 수 있다.                
  따라서 서버쪽 코드가 변하더라도 클라이언트 코드를 따로 수정할 필요가 없다.            
     
   
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
 
