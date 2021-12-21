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
  
**IANA에 등록하는 것은 필수인가? 🤔**     
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

## Self-descriptive과 HATEOAS의 독립적 진화   
   
**Self-descriptive**       
* 확장 가능한 커뮤니케이션      
* 서버나 클라이언트가 변경되더라도  오고가는 메시지는 언제나 self-descriptive 하므로 언제나 해석 가능하다.    
   
**HATEOAS**      
* 애플리케이션 상태 전이의 late binding        
* 어디서 어디로 전이가 가능한지 미리 결정되지 않는다.         
* 어떤 상태로 전이가 완료되고 나서야 그 다음 전이 될 수 있는 상태가 결정된다.           
* 쉽게 말해서 링크는 동적으로 변경될 수 있다.(클라이언트가 수정안해도 값 받아서 연결)    

# REST API가 어려운 이유 

||흔한 웹 페이지|HTTP API|
|-|----------|--------|  
|Protocol|HTTP|HTTP| 
|커뮤니케이션|사람-기계|기계-기계|   
|Media Type|HTML|JSON|  
   
* 웹페이지는 사람이 보고, 이를 위해 HTML로 이루어져있다.   
* HTTP API는 기계가 보고, 이를 속도 + 쉽게 처리하기 위해 JSON을 사용한다.    


||HTML|JSON|
|-|----------|--------|  
|Hyperlink|됨(a 태그등)|정의되어있지 않음|   
|Self-descriptive|됨(HTML 명세)|불완전*|     
         
* **하이퍼링크 + self-descriptive를 처리할 수 없다.**              
* JSON 문법은 정의되어있으나 내부 Key를 해석할수 없어 불완전하다.           
* 이를 해결하기 위해서 결국 API 문서를 만들어야 했다.     
 
## REST API 어려운 이유 예시(HTML VS JSON)
  
![image](https://user-images.githubusercontent.com/50267433/146887929-8643e992-78b9-44a1-a9b7-ab2f8d7f61da.png)

### HTML      
> HTML은 메시지에 대한 완벽한 해석이 가능하며, 상태 전이도 가능하다.     
 
![image](https://user-images.githubusercontent.com/50267433/146887974-68889726-ced6-400e-b599-0382f447cbdd.png)
 
* HTML은 태그를 이용해서 요소에 대한 해석 + 상태 전이를 표현할 수 있다.      
 
___  

### JSON   
> JSON은 메시지에 대한 완벽한 해석이 가능하지 않으며 일반적인 방법으로는 상태 전이도 불가능하다.      
 
![image](https://user-images.githubusercontent.com/50267433/146888083-c83624c5-3fbe-46ff-ac68-de55ab150188.png)

* JSON은 대부분의 요소들에 대해서 해석이 가능하나 정작 JSON 요소들에 대해서 표준이 아닌 이상 해석이 힘들다.        
* 또한 일반적인 경우, 상태 전이 즉, HATEOAS 를 지원하기 힘들다.    

____

## REST API로 고쳐보자  
### SELF-DESCRIPTIVE 
 
* 커스텀 미디어타입을 도입한다.    
* Link 헤더를 도입하여 profile 명세서를 제공한다.    
 
### HATEOAS  

* JSON 내부에 **Key : URI**을 이용하여 하이퍼링크를 남긴다.            
* Key의 네이밍을 복수형으로 선언하여 여러 하이퍼링크를 남겨줄 수 있다.        
* 당연하게도, 커스텀 미디어 타입을 이용해서 Key의 네이밍을 자유롭지만 표현 가능하게 할 수 있다.    
* Link 헤더를 도입하여 바로 다음 하이퍼 링크를 제공해줄수 있다.  
* 결국에는 HATEOAS 같은경우 data, 헤더를 이용해서 모두 표현 가능하다.     
  
# 질문 

* 하이퍼링크는 꼭 URI여야 하는가? : 상관없다, 
* INAN은 등록되어야하는가? : 사내에서 사용한다던가, 사용자들이 모두 알고 있으면 굳이 안해도 된다. 그러나 장점으로 하는게 좋다.  
* 우리가 만드는 API는 꼭 REST API를 사용해야 하는가? : 시스템 전체를 통제할 수 있다고 생각하거나 진화에 관심없다면, REST에 대해 따지느라 시간 낭비하지마라   
     * 즉, 클라이언트 개발자를 내가 컨트롤하거나, API를 독단적으로 개발할 수 있어 맘대로 변경 가능한 경우는 상관없다.     

# 정리 
* 오늘날 대부분의 REST API는 REST 아키텍처를 지키지 않고 있다.      
* REST 제약조건 중에서 특히 Self-descriptive 랑 HATEOAS를 지키지 않고 있다.     
* REST는 긴 시간에 걸쳐 진화하는 웹 애플리케이션을 위한 것이다.     
* REST를 따를 것인지는 API를 설계하는 이들이 스스로 판단하여 결정해야 한다.      
* REST를 따르겠다면, Self-descriptive와 HATEOAS를 만족시켜야한다.     
    * Self-descriptive 는 custom media type이나 profile link relation 등으로 만족시킬 수 있다.  
    * HATEOAS는 HTTP 헤더나 본문에 링크를 담아 만족시킬 수 있다.    
* REST를 따르지 않겠다면, REST를 만족하지 않는 REST API를 뭐라고 부를지 결정해야할 것이다.        
    * HTTP API라고 부를수도 있고     
    * 그냥 이대로 REST API라고 부를수도 있다.     
