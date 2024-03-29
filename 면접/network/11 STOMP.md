# STOMP(Simple Text Oriented Messaging Protocol) 보충 설명   
WebSocket 프로토콜은 단순히 문자열을 주고 받는 역할만 수행한다.      
     
STOMP은 메세징 전송을 효율적으로 하기 위해 탄생한 서브 프로토콜로써 WebSocket 위에서 동작한다.  
`pub/sub` 구조로 메세지를 전송하고 받는 부분이 정해져 있어서 개발자 입장에서 명확하게 인지하고 개발할 수 있는 이점이 있다.   
**즉, 클라이언트와 서버가 전송할 메세지의 `유형`, `형식`, `내용`들을 정의하는 매커니즘이다.**          
                
## 메시지 
STOMP는 HTTP에서 모델링되는 Frame 기반의 프로토콜로써 `명령`, `헤더`, `바디`로 구성되어있다.          
더불어, **Text 지향 프로토콜로 `Message Payload`에는 `Text or Binary 데이터`를 포함 할 수 있다.**       
  
```console
COMMAND
header1:value1
header1:value1

bodybodybodybody^@
```  
   
**명령**      
* CONNECT       
* SEND      
* SUBSCRIBE     
* DISCONNECT       
            
**헤더**               
* 메시지에 헤더 값을 이용한 작업을 처리할 수 있다.                 
* **destination :** 이 헤더로 메세지를 보내거나(SEND), 구독(SUBSCRIBE)할 수 있다.      
* **subscription-id :** 불분명한 메시지를 전송하지 못하도록 하는 헤더이다.        
    서버의 모든 메세지는 특정 클라이언트 구독에 응답하여야 하고, 클라이언트 구독의 `id`헤더와 일치해야 한다.      
    
**바디**   
* 헤더와 바디는 빈 라인으로 구분한다.      
* 바디의 끝 부분은 NULL 문자 `^@`로 설정한다.        

### 전송

```console
SEND
destination: /pub/chat
content-type: application/json

{"chatRoomId": 5, "type": "MESSAGE", "writer": "clientB"} ^@
```

### 구독  

```console
SUBSCRIBE
destination: /topic/chat/room/5
id: sub-1

^@
```

### 브로드 캐스팅 

```console
MESSAGE
destination: /topic/chat/room/5
message-id: d4c0d7f6-1
subscription: sub-1

{"chatRoomId": 5, "type": "MESSAGE", "writer": "clientB"} ^@
```
  
STOMP 서버는 모든 구독자에게 메세지를 Broadcasting하기 위해 MESSAGE COMMAND를 사용할 수 있다.      
서버는 내용을 기반(chatRoomId)으로 메세지를 전송할 broker에 전달한다. (topic을 sub로 보아도 될 것 같다.)  
   
## PUB/SUB

![다운로드 (1)](https://user-images.githubusercontent.com/50267433/148089892-20431afd-930a-40d0-ae72-42aa15db833d.jpeg)

STOMP는 Publish-Subscribe 매커니즘을 제공한다.      
즉 Broker를 통해 타 사용자들에게 메세지를 보내거나 서버가 특정 작업을 수행하도록 메세지를 보낼 수 있게 된다.   
만약 Spring에서 지원하는 STOMP를 사용하면 Spring WebSocket 애플리케이션은 STOMP Broker로 동작하게 된다.           
       
* **채팅방 생성 :** pub / sub 구현을 위한 Topic이 생성됨      
* **채팅방 입장 :** Topic 구독    
* **채팅방에서 메세지를 송수신 :** 해당 Topic으로 메세지를 송신(pub), 메세지를 수신(sub)       
                            
Spring에서의 STOMP는 많은 기능을 지원한다.   
예를 들어, `Simple In-Memory Broker`를 이용해 SUBSCRIBE 중인 다른 클라이언트들에게 메세지를 보내준다.     
`Simple In Memory Broker`는 클라이언트의 SUBSCRIBE 정보를 자체적으로 메모리에 유지하는 기술이다.            
또한, `RabbitMQ`, `ActiveMQ`같은 외부 메세징 시스템을 `STOMP Broker`로 사용할 수 있도록 지원한다.         
   
![다운로드](https://user-images.githubusercontent.com/50267433/148092262-e64c41b5-dad4-4634-942e-f203895964a7.png)  
        
구조적인 면을 보자면, 스프링은 메세지를 Broker에게 전달하고,             
Broker는 WebSocket으로 연결된 클라이언트에게 메세지를 전달하는 구조다.               
이와 같은 구조 덕분에 HTTP 기반의 보안 설정과 공통된 검증 등을 적용할 수 있게 된다.  
   
