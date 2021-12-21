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

# 원격 API가 꼭 Rest API여야 하는가?      
아니다, 단 시스템 전체를 통제할 수 있다고 생각하거나(클라이언트개발자를 내가 조종가능, API맘대로 변경가능)      
진화에 관심없다면, REST에 대해 따지느라 시간 낭비하지마라  
   
# 일단 왜 API는 REST가 잘 안되나(일반적인 웹과 비교해보자)   

![image](https://user-images.githubusercontent.com/50267433/146887581-c51e032d-de0c-40d6-be67-2f6988e75790.png)
  
* 웹페이지는 사람이 보고, 이를 위해 HTML로 이루어져있다.   
* HTTP API는 기계가 보고, 이를 속도 + 쉽게 처리하기 위해 JSON을 사용한다.    
  
아 문제는 JSON이였구나..  

![image](https://user-images.githubusercontent.com/50267433/146887697-e00c5c09-58d1-4b52-be5c-3c0e6a02f0ad.png)
  
* 하이퍼링크 + self-descriptive를 처리할 수 없다.     
* 문법은 정의되어있으나 그자체 의믜를 해석이 가능한게 없어서 불완전하다(문버 해석가능, 문법 의미 해석 불가능)   
* 이를 해결하기 위해서 우리는 API 문서를 만들었다.   

![image](https://user-images.githubusercontent.com/50267433/146887929-8643e992-78b9-44a1-a9b7-ab2f8d7f61da.png)
   
HTML은 완벽히 해석 가능한가? 가능하다. / HATEOAS도 가능하다(전이 가능)     
![image](https://user-images.githubusercontent.com/50267433/146887974-68889726-ced6-400e-b599-0382f447cbdd.png)
   
JSON은 온전한 해석이 가능하지 않다.(객체 키들의 뜻은) / HATEOAS도 전이가 불가능하다.   

![image](https://user-images.githubusercontent.com/50267433/146888083-c83624c5-3fbe-46ff-ac68-de55ab150188.png)

# 그런데 Self-descriptive과 HATEOAS가 독립적 진화에 어떻게 도움이될까?   
  
**Self-descriptive**       
* 확장 가능한 커뮤니케이션      
* 서버나 클라이언트가 변경되더라도  오고가는 메시지는 언제나 self-descriptive 하므로 언제나 해석가능하다.    
 
**HATEOAS**    
* 애플리케이션 상태 전이의 late binding       
* 어디서 어디로 전이가 가능한지 미리 결정되지 않는다.       
* 어떤 상태로 전이가 완료되고 나서야 그 다음 전이 될 수 있는 상태가 결정된다.         
* 쉽게 말해서 링크는 동적으로 변경될 수 있다.(클라이언트가 수정안해도 값 받아서 연결)  

# REST API로 고쳐보다  
## SELF-DESCRIPTIVE 
### 
![image](https://user-images.githubusercontent.com/50267433/146888818-f2e3615f-fcb2-438e-ae2b-61a1c5ab9eb3.png)

![image](https://user-images.githubusercontent.com/50267433/146888786-04ef325f-89e5-4d18-b45b-3c1accc8a937.png)

### 

![image](https://user-images.githubusercontent.com/50267433/146888874-44fab28d-a7f4-4999-859a-6d66e0018cae.png)
![image](https://user-images.githubusercontent.com/50267433/146888919-e6f3db18-2542-4e71-b51a-a17d9473ead1.png)

## HATEOAS
### 

![image](https://user-images.githubusercontent.com/50267433/146888969-6a6139f4-9d02-4da2-955c-da529011a77c.png)

### data로 
![image](https://user-images.githubusercontent.com/50267433/146889041-8f8d41f2-5e14-420b-af1e-ec9c2cb1c0c8.png)

### data로2

![image](https://user-images.githubusercontent.com/50267433/146889118-839a2d5d-5ea0-40b1-a7cb-4d8ad3ac7ead.png)

### HTTP 헤더로  
![image](https://user-images.githubusercontent.com/50267433/146889184-3f1ef60c-d416-4af0-ae5e-e024c53879e1.png)


결국에는 HATEOAS 같은경우 data, 헤더를 이용해서 모두 표현가능하다.   

![image](https://user-images.githubusercontent.com/50267433/146889236-372fecf3-cc3d-467e-a455-472af622da6d.png)

상관없다.  

![image](https://user-images.githubusercontent.com/50267433/146889277-e58ea19e-7951-4093-8ec1-1b4fc065384f.png)

사내에서 사용한다던가, 사용자들이 모두 알고 있으면 굳이 안해도 된다.  

![image](https://user-images.githubusercontent.com/50267433/146889358-a6c7e421-3666-4009-afb9-e667248d732c.png)

그러나 위와 같은 장점으로 하는게 좋다.  

# 정리 

![image](https://user-images.githubusercontent.com/50267433/146889441-4499c36e-c04f-4bff-aeed-c9df0ed19c37.png)
   
마지막 문구는 현재 RestFul이라고 부른다.   

 
