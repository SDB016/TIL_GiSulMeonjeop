# REST API  

* REST API : REST 아키텍처 스타일을 따르는 API   
* REST : 분산 하이퍼미디어 시스템(웹)을 위한 아키텍처 스타일   
* 아키텍처 스타일 : 제약조건의 집합 
  
즉, 제약조건을 모두 지켜야 REST를 따른다고 말할 수 있다.   
      
**REST를 구성하는 스타일(아키텍처 스타일 + 하이브리드 아키텍처 스타일)**    
* client-server
* stateless 
* cache 
* **uniform interface**  
* layer system
* code-on-demand(optional)  

## Client-Server
## Stateless
## Cache
## Uniform Interface
## Layer System  
## code-on-demand  
서버에서 코드를 보내면 클라이언트에서 바로 실행가능해야한다(HATEOS)  


* selef-descriptive messages   
    * 메시지는 스스로 설명해야한다.  
    * ![image](https://user-images.githubusercontent.com/50267433/146884353-c657795f-8331-45e6-91e2-ca98716d94f8.png)
    * 목적지가 빠져있었다. 
    * ![image](https://user-images.githubusercontent.com/50267433/146884418-138133b8-9290-457a-ac90-2d8d16264720.png)
    * ![image](https://user-images.githubusercontent.com/50267433/146884471-8e8b4987-149b-4238-a36f-1e5f467dbca5.png)
    * 이게 어떤 문법으로 작성되었는지 모른다.   
    * ![image](https://user-images.githubusercontent.com/50267433/146884501-ce74a85a-32bd-4792-ae00-e0dd3fd7de4d.png) 
    * ![image](https://user-images.githubusercontent.com/50267433/146884536-77e03541-819e-4e57-9a0c-9bc61af256ef.png)
    * json-patch-json 의 명세를 기술해서, op와 path가 어떤 의미인지 알게끔한다.    
    * 모든 요소에 대해서 해석이 가능해야한다.    
 
* hypermedia as the engine of application state(hateoas)  
    * 애플리케이션의 상태는 Hyperlink를 이용해 전이되어야 한다.  
    * ![image](https://user-images.githubusercontent.com/50267433/146884796-1ae90e1e-ade8-44f0-ad61-5120d1fd7e2a.png)
    * 예를들면, HTTP만을 이용해서라도 상태들이 전이될 수 있어야한다.(페이지의 다음링크 존재가 보장되어야한다)     
    * ![image](https://user-images.githubusercontent.com/50267433/146884907-3fbc966a-4b2a-44f5-a55a-13f9e98d3705.png)
    * HTML을 반환한다면, 다음 링크를 넘겨줄 수 있어야한다.  
    * ![image](https://user-images.githubusercontent.com/50267433/146884987-618c0432-2994-49c8-820b-a3735a08cdb1.png)
    * JSON에서도 Link라는 헤더를 이용하면 된다.  
    * Link 헤더가 표준으로 문서가 나와있기에 이를 온전히 해석해서 다른 상태로 전이하게끔 한다.  
  
그럼 왜 Uniform 인터페이스를 해야하는가?     
   
**독립적 진화**      
* 서버와 클라이언트가 각각 독립적으로 진화한다.       
* 서버의 기능이 변경되어도 클라이언트를 업데이트할 필요가 없다.      
* REST를 만들게 된 계기 : HOW DO IMPORVE HTTP WITHOUT BREAKING THE WEB   

# 웹    

* 웹 페이지를 변경했다고 웹 브라우저를 업데이트할 필요가 없다.     
* 웹 브라우저를 업데이트했다고 웹 페이즈를 변경할 필요도 없다.    
* HTTP 명세가 변경되어도 웹은 잘 동작한다.        
* HTML 명세가 변경되어도 웹은 잘 동작한다.     
* 반응형으로 페이지가 깨질수있지만, 동작은 한다.(기능은 된다는 것)   

   
# 상호 운용성에 대한 집착  
* Referer 오타지만 안고침      
* charset 잘못 지은 이름이지만 안고침  
* HTTP 상태 코드 416포기함(I'm teapot)    
* HTTP/0.9 아직도 지원함(크롬, 파이어폭스)  
 
# REST가 웹의 독립적 진화에 도움을 주엇나     
* HTTP에 지속적으로 영향을 주었다.     
* Host헤더 추가       
* 길이 제한을 다루는 방법 명시(414 URI TOO LONG 등)       
* URI에서 리소스의 정의가 추상적으로 변경되었다.(식별하고자하는 무언가)    
* 기타 HTTP와 URI에 많은 영향을 줌        
* HTTP/1.1 명세 최신판에서 REST 에 대한 언급이 들어간다.     

# 그럼 REST는 성공했는가?   
* REST는 웹의 독립적 진화를 위해 만들어졌다.     
* 웹은 독립적으로 진화하고 있다.    

# 그런데 REST API는?   
  
* REST API는 REST 아키텍처 스타일을 따라야한다.     
* 오늘날 스스로 REST API라고 하는 API들은 대부분이 REST 아키텍처 스타일을 따르지 않는다.    
    
REST API도 제약조건을 다 지켜야하는건가? 응 지켜야됭   
  
# 원격 API가 꼭 Rest API여야 하는가?      
아니다, 단 시스템 전체를 통제할 수 있다고 생각하거나(클라이언트개발자를 내가 조종가능, API맘대로 변경가능)      
진화에 관심없다면, REST에 대해 따지느라 시간 낭비하지마라  

# 그럼이제 어떻게 할까?  
* REST API를 구현하고 REST API라고 부른다.   
* REST API를 구현하지 않고 HTTP API라고 부른다.       
* REST API가 아니지만 REST API라고 부른다.(현재 상태)  
  
그래서 REST API를 만든사람이 이렇게 말한다.     
제발 제약 조건을 따르던지 아니면 다른 단어를 사용해줘    
그래서 REST 명세를 완벽히 지킨 API를 RestFul API이다.    
   
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

07 RESTAPI    
=======================    
시대가 변하면서 다양한 브라우저와 모바일 기기가 탄생하고 있다.         
이러한 다양한 기기들을 단일 서버로 데이터를 관리하여 유연하게 클라이언트 영역을 대응할 수 있는 방법이 있는데, 바로 REST 서버이다.           
클라이언트는 단지 REST 서버를 통해 데이터를 받아와서 각 기기별로 대응하면 된다.               
                
REST는 웹의 장점을 극대화하는 통신 네트워크 아키텍처다.            
REST의 구현 원칙을 제대로 지키는 시스템을 RESTful 이라고 한다.             
현재 웹에서 사용하는 대부분의 데이터 통신이 REST API라고 해도 과언이 아니다.        
                           
# 배경지식  
## REST 소개    
REST 는 웹과 같은 **분산 하이퍼미디어 시스템에서 사용하는 통신 네트워크 아키텍처**로, 네트워크 아키텍처의 원리 모음이다.       
                     
**웹은 전송 방식으로 `HTTP`,**      
**식별 방법으로 `URI`를 사용한다.**    
       
HTTP는 웹에서 `GET`, `POST`, `PUT`, `DELETE` 등의 메소드를 사용하여 정보를 주고받는 프로토콜이다.               
REST는 **HTTP 와 URI의 단순하고 간결한 장점을 계승화한 네트워크 아키텍처**입니다.                 
따라서 다양한 요구사항에 대응하여 때로는 단순하게,           
때로는 서버와 클라이언트가 서로 통신하는 리소스에 대해 복잡한 방식으로 상호작용할 수 있다.                     
           
REST는 다음과 같은 목적으로 만들어졌다.      
          
* 구성요소 상호작용의 규모 확장성        
* 인터페이스 범용성            
* 구성요소의 독립적인 배포          
* 중간적 구성요소를 이용한 응답 지연 감소, 보안 강화, 레거시 시스템 인캡슐레이션      
 
**URI(Uniform Resouce Identifier, 통합자원식별자)**    
```
URI(Uniform Resouce Identifier, 통합자원식별자)는 인터넷에서 특정 자원을 나타내는 유일한 주솟값입니다.   
REST API 는 URI를 사용하여 자원을 처리합니다.     
```

## RESTful 제약조건    
앞서 REST의 구현 원칙을 제대로 지키면서 REST 아키텍처를 만드는 것을 RESTful 이라고 설명했습니다.          
다음은 RESTful 제약조건입니다.         
      
* **클라이언트-서버** :           
이 제약 조건의 기본 원칙은 관심사의 명확한 분리입니다.          
관심사의 명확한 분리가 선행되면 서버의 구성요소가 단순화되고 확장성이 향상되어 여러 플랫폼을 지원할 수 있습니다.          
         
* **무상태성** :        
서버에 클라이언트의 상태 정보를 저장하지 않는 것을 의미합니다.             
단순히 들어오는 요청만 처리하여 구현을 더 단순화 합니다.         
단, 클라이언트의 모든 요청은 서버가 요청을 알아듣는데 필요한 모든 정보를 담고 있어야 합니다.        
      
* **캐시 기능** :     
클라이언트의 응답을 캐시할 수 있어야 합니다.       
앞에서 HTTP의 장점을 그대로 계승한 아키택처가 REST라고 했습니다.        
따라서 HTTP의 캐시 기능도 적용할 수 있습니다.      
       
* **계층화 시스템** :       
서버는 중계 서버(게이트웨이, 프록시)나 로드 밸런싱, 공유 캐시등의 기능을 사용하여 확장성 있는 시스템을 구성할 수 있습니다.        
이 제약조건은 선택적 제약 조건입니다.       
    
* **코드 온 디맨드** :   
클라이언트는 서버에서 자바 애플릿, 자바스크립트 같은 실행 코드를 전송받아 기능을 일시적으로 확장할 수 있습니다.   
이 제약조건은 선택적 제약 조건입니다.         
    
* **인터페이스 일관성** :    
URI로 지정된 리소스에 균일하고 통일된 인터페이스를 제공합니다.         
아키텍처를 단순하게 분리하여 단순하게 만들 수 있습니다.      

### 인터페이스 일관성        
인터페이스 일관성은 세부 원칙을 가지고 있습니다.       
인터페이스 일관성이 잘 지켜졌는지에 따라 REST를 제대로 사용했는지 판단할 수 있습니다.      
인터페이스 일관성에는 다음 4가지가 존재합니다.        
         
1. 자원 식별                  
2. 메시지를 통한 리소스 조작             
3. 자기 서술적 메시지           
4. 애플리케이션 상태에 대한 엔진으로서의 하이퍼미디어               
    
___ 
    
**자원 식별** :          
웹 기반의 REST에서 리소스 접근을 주로 URI를 사용한다는 것을 나타냅니다.         
즉, 각각의 리소스는 요청에서 식별가능합니다.        
 
```
http://localhost:8080/resource/1
```
예를 들어 URI에서 정보는 ```resouce```, 유일한 구분자는 ```1```로 식별합니다.         
   
___
   
**메시지를 통한 리소스 조작** :       
클라이언트가 특정 메시지나 메타데이터를 가지고 있으면 자원을 수정, 삭제하는 충분한 정보를 갖고 있는 것으로 볼 수 있습니다.       

```
http://localhost:8080/resource/1
content-type: application/json    
```   
예를 들어 코드에서 ```content-type``` 은 리소스가 어떤 형식인지 지정합니다.    
리소스는 HTML, XML, JSON 등 다양한 형식으로 전송됩니다.     
    
___    
        
**자기 서술적 메시지** :    
각 메시지는 자신을 어떻게 처리해야 하는지 충분한 정보를 포함해야 합니다.     
웹 기반의 REST에서는 HTPP Method 와 Header 를 활용합니다.       

```
GET http://localhost:8080/resource/1     
content-type: application/json    
```   
예를 들어 GET 메서드를 활용하여 ```/resource/1```의 정보를 받아온다는 것을 표현했습니다.     
    
___    
    
**HATEOAS** :     
애플리케이션 상태에 대한 엔진으로서의 **하이퍼미디어**         
이는 클라이언트에 응답할 때 단순히 **결과 데이터만 제공해주기보다는 URI를 함께 제공해야한다는 원칙**입니다.        
하이퍼텍스트 링크처럼 **관련된 리소스 정보를 포함합니다.**      
          
REST의 제약조건들을 제대로 지키면서 REST 아키텍처를 만드는 것을 RESTful 이라고 합니다.    
특히 제약 조건 중 **하이퍼텍스트를 포함**하고 **자기 서술적**이며 **인터페이스 일관성을 통해 리소스에 접근하는 API**여야 RESTFful 하다 할 수 있습니다.  
즉, 자기 자신이 어떻게 처리되는지에 대한 충분한 정보, 관련된 리소스를 하이퍼텍스트 링크로 포함시켜야 'RESTful 하구나' 생각할 수 있습니다.         
              
여기서 HATEOAS는 **응답 데이터와 관련된 하이퍼미디어 링크를 추가**하여 사이트의 REST 인터페이스를 **동적으로 탐색**하도록 도와줍니다.                 
                  
* 클라이언트는 관련된 특정 동작에 따라 탐색할 만한 URI 값을 알 수 있습니다.                     
URI는 resource 까지 포함하므로 더 명확하게 예측이 가능합니다.                  
          
* 키 값이 변하지 않는 한 URI가 변경되더라도 동적으로 사용할 수 있습니다.             
따라서 서버쪽 코드가 변하더라도 클라이언트 코드를 따로 수정할 필요가 없습니다.          
     
## REST API 설계하기       
REST API는 다음과 같이 구성합니다.        
     
* 자원 : URI   
* 행위 : HTTP 메서드   
* 표현 : 리소스에 대한 표현 (HTTP Message Body)       
  
### URI 설계    
**URI**는 `URL`을 포함하는 개념입니다.      
        
**URL(Uniform Resouce Locator, 파일식별자)**   
```
URL(Uniform Resouce Locator, 파일식별자) 은 인터넷상에서 자원, 즉 특정 파일이 어디에 위치하는지 식별하는 방법입니다.   
```

**URL 예시**   
```  
http://localhost:8080/api/book.pdf      
```  
URL은 웹상의 파일 위치를 표현합니다.    
    
**URI 예시**   
```  
http://localhost:8080/api/book/1         
```   
URI는 웹에 있는** 자원의 이름**과 **위치**를 식별합니다.         
       
그렇기에 URL은 URI의 하위 개념입니다.    
URL이 리소스를 가져오는 방법에 대한 위치라면 URI는 문자열을 식별하기 위한 표준입니다.      
          
### 명사를 사용해라   
      
```
http://localhost:8080/api/read/books   
```   
URI은 명사를 사용해야 하며 동사를 피해야합니다.          
위 같은 코드는 ```/read/```라는 동사가 들어 있으므로 좋지 못한 코드라고 할 수 있습니다.   
    
**동사를 피해야하는 이유는** HTTP Message 에서 이미 자원에 대한 설명 및 동작이 이루어집니다.        
만약, `/read/`를 사용했지만, 데이터를 삭제한다면? 이는 URI의 의미 자체를 없애는 행위입니다.      
    
```
GET http://localhost:8080/api/books   
content-type: application/json
```    
이처럼 동사를 표현할 때는 HTTP 메서드인 GET, POST, PUT, DELETE 등으로 대체해야 합니다.         
하지만 모든 경우에 완벽하게 호환되지는 않습니다.       
세부적인 동사의 경우 URI에 포함될 수 밖에 없습니다.        
앞의 URI 설계에 대한 원칙은 어디까지나 불필요한 동사를 URI에 포함하는 것을 지양해야 한다는 것이지    
**완전히 배제시킨다는 것은 아닙니다.**         
        
### 복수형을 사용해라     
URI에서는 명사에 단수형보다는 복수형을 사용해야 합니다.        
```/book```도 물론 명사고 사용가능하지만       
```/books```로 리소스를 표현하면 컬렉션으로 명확하게 표현할 수 있어 확장성 측면에서 더 좋습니다.     
주로 사용되는 인터페이스는 Set, List, Queue, Deque입니다.         
이러한 컬렉션은 객체의 단일 단위, 즉 그룹을 나타냅니다.      
  
```javascript    
{
     books: [
          {
               book: ...
          },
          {
               book: ...
          },
          {
               book: ...
          },
     ]
}
```
그리고 컬렉션으로 URI를 사용할 경우 컬렉션을 한번 더 감싼 중첩 형식을 사용하는 것이 좋습니다.    
만약 중첩하지 않고 바로 컬렉션을 반환하면 추후 수정할 때나 확장할 때 번거롭게 됩니다.    
      
예를 들어 중첩하지 않고 하나의 ```books``` 컬렉션만 보내는 도중 다른 요구사항이 있다고 가정합시다.    
요구사항이 전혀 다른 ```stores``` 컬렉션을 추가하는 겁니다.    
기존의 형태가 ```키값 + 컬렉션``` 으로 중첩된 형태가 아니기 때문에 ```stores``` 컬렉션을 추가하기 위해 기존의 형태가 깨지게 됩니다.     
그렇게 되면 서버에서 API 스펙을 수정하게 되고 클라이언트도 수정된 API 스펙에 맞게 코드를 수정해야합니다.   

```javascript   
{
     _embedded: [
          {
               books: [
                    {
                         book: ...
                    },
                    {
                         book: ...
                    },
                    {
                         book: ...
                    },
               ]
          },
          {
               stores: [
                    {
                         store: ...
                    },
                    {
                         store: ...
                    },
                    {
                         store: ...
                    },
               ]
          }          
     ]
}
```
위 코드는 앞서 말한 방식대로 작성한 코드입니다.       
```-embedded : []``` 내부에 기존 컬레션의 키 값이 유지되게 보낼 경우        
서버의 API 스펙이 변경되더라도 클라이언트는 따로 코드를 수정할 필요가 없습니다.      
   
이렇게 확장성을 나타내는 (중첩 형태를 나타내는) ```_embedded```로 데이터를 감싸서 여러 키값을 한번에 보낼 수 있습니다.      
이런 형식을 유지하면 뒤늦게 데이터가 추가되어도 기존에 제공한 ```books``` 데이터와 관련된 부분을 수정하지 않아도 됩니다.           

### 슬래시 구분자(/)는 계층 관계를 나타내는 데 사용해라 
```
http://restapi.example.com/houses/apartments
http://restapi.example.com/animals/mammals/whales
```

### URI 마지막 문자로 슬래시(/)를 포함하지 않는다.
```
http://restapi.example.com/houses/apartments/ (X)
http://restapi.example.com/houses/apartments  (0)
```
URI에 포함되는 모든 글자는 리소스의 유일한 식별자로 사용되어야 하며      
URI가 다르다는 것은 리소스가 다르다는 것이고,      
역으로 리소스가 다르면 URI도 달라져야 합니다.      
REST API는 분명한 URI를 만들어 통신을 해야 하기 때문에 혼동을 주지 않도록       
**URI 경로의 마지막에는 슬래시(/)를 사용하지 않습니다.**   


### 하이픈(-)은 URI 가독성을 높이는데 사용
URI를 쉽게 읽고 해석하기 위해, 불가피하게 긴 URI경로를 사용하게 된다면    
하이픈을 사용해 가독성을 높일 수 있습니다.   

### 밑줄`(_)`은 URI에 사용하지 않는다.    
글꼴에 따라 다르긴 하지만 밑줄은 보기 어렵거나 밑줄 때문에 문자가 가려지기도 합니다.      
이런 문제를 피하기 위해 밑줄 대신 하이픈(-)을 사용하는 것이 좋습니다.(가독성)       

### URI 경로에는 소문자가 적합하다.
URI 경로에 대문자 사용은 피하도록 해야 합니다.     
대소문자에 따라 다른 리소스로 인식하게 되기 때문입니다.      
RFC 3986(URI 문법 형식)은 URI 스키마와 호스트를 제외하고는 대소문자를 구별하도록 규정하기 때문이지요.   
        
여담으로, `I`, `O` 같은 단어들을 사용했을 때 평소에는 괜찮은데       
비슷한 단어와 헷갈릴 수 있다면 되도록 사용을 줄이는 편이 좋다.         
    
### 파일 확장자는 URI에 포함시키지 않는다.
```
http://restapi.example.com/members/soccer/345/photo.jpg (X)
```
REST API에서는 메시지 바디 내용의 포맷을 나타내기 위한 파일 확장자를 URI 안에 포함시키지 않습니다.    
`Accept header`를 사용하도록 합시다. -> `accept-header : application/json`
```
GET / members/soccer/345/photo HTTP/1.1 Host: restapi.example.com Accept: image/jpg
```

### 리소스 간의 관계를 표현
REST 리소스 간에는 연관 관계가 있을 수 있고, 이런 경우 다음과 같은 표현방법으로 사용합니다.
```
             /리소스명/리소스 ID/관계가 있는 다른 리소스명  
ex)    GET : /users/{userid}/devices (일반적으로 소유 ‘has’의 관계를 표현할 때)   
```   
만약에 관계명이 복잡하다면 이를 서브 리소스에 명시적으로 표현하는 방법이 있습니다.       
예를 들어 사용자가 ‘좋아하는’ 디바이스 목록을 표현해야 할 경우 다음과 같은 형태로 사용될 수 있습니다.    

```
GET : /users/{userid}/likes/devices (관계명이 애매하거나 구체적 표현이 필요할 때)   
```    
      
### 행위 설계             
`/books`의 경우 book의 목록을 표현한다는 기본 전제가 깔려있습니다.         
따라서 `/books`로 URI를 표현하면 기본적으로 복수를 나타내며 작게는 하나의 단위를 나타낼 수 있게 됩니다.        
즉, `/books/{단일값}`은 books 의 목록 중 특정 book을 사용합니다.        
이제 원하는 행위에 따라 동사를 선택적으로 사용합니다.        
        
`/books` 자체가 복수의 book을 의미하므로 books를 게시판에 표현할 때 페이징을 처리하는 값을 추가로 제공할 수도 있습니다.    
추가 값으로 페이지, 크기, 정렬, 등의 파라미터를 지정할 수 있습니다.      
아래와 같이 JPA의 Pageable의 프로퍼티 값을 그대로 사용할 수 있습니다.      

```
GET http://localhost:8080/api/books?page=0&size=10&sort=desc
content-type: application/json    
```    
page, size, sort 파라미터를 따로 지정하지 않으면 서버에서 기본으로 설정한 값으로 반환됩니다.   

### HTTP METHOD
|METHOD|역할|  
|------|----|    
|POST|POST를 통해 해당 URI를 요청하면 리소스를 생성합니다.|    
|GET|GET를 통해 해당 리소스를 조회합니다. 리소스를 조회하고 해당 도큐먼트에 대한 자세한 정보를 가져온다.|    
|PUT|PUT를 통해 해당 리소스를 수정합니다.|	    
|DELETE|DELETE를 통해 리소스를 삭제합니다.|     



