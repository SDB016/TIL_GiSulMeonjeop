# TCP와 UDP
## TCP란? 
## UDP란? 

## TCP 3 way handshake 

1. 클라이언트는 서버로부터 연결을 위해 SYN 을 보낸다.    
2. 서버는 클라이언트로부터 확인 메시지 ACK과 서버의 연결을 위한 ACK을 보낸다.   
3. 클라이언트는 서버에게 연결완료라는 ACK을 보낸다.  

## TCP 4 way handshake
  
1. 클라이언트가 서버로 연결을 종료하겠다는 FIN 플래그를 전송한다.   
2. 서버는 클라이언트에게 ACK 메시지를 보내고 자신의 남은 통신이 끝날때까지 기다린다.   
3. 서버가 통신이 끝나면 클라이언트로 FIN을 보낸다.  
4. 클라이언트는 확인했다는 의미로 서버에게 ACK을 보내면 연결이 종료가 완료된다.    
5. 단, 클라이언트는 FIN을 받았다고 소켓을 닫으면 남은 데이터를 못받을 수 있어서 잠깐 TOME_OUT 대기한다.  

# HTTP
## HTTP란?  
> HyperText Transfer Protocol
    
웹 상에서 클라이언트와 서버 간에 요청/응답(request/response)으로 정보를 주고 받을 수 있는 프로토콜    

## HTTPS란?  
    
웹 통신 프로토콜인 HTTP에 보안 프로토콜인 SSL이나 TLS를 올린 형태의 프로토콜         
  
## HTTPS가 필요한 이유?

1. HTTP 는 평문 통신이기 때문에 도청이 가능하다.
2. 통신 상대를 확인하지 않기 때문에 위장이 가능하다.
3. 내용의 정확성을 증명할 수 없기 때문에 변조가 가능하다.

## HTTPS의 원리 

1. 클라이언트 : 랜덤값 + 브라우저가 적용할 수 있는 암호화 방식 후보 리스트 전달
2. 서버 : 랜덤값 + 클라이언트가 보낸 리스트중 적용 가능한 암호화 방식 1개 채택 + SSL CA 인증서 전달
3. 클라이언트 : CA가 올바른지 확인, CA에 담긴 Public key로 pre master secret을 암호화해서 요청
4. 서버 : Private key로 해독한 후, 앞으로 사용할 대칭키를 만들고 클라이언트에게 전달
5. 이후부터 : 클라이언트와 서버간에 대칭키를 통해서 통신

## GET VS POST   

* GET : 주로 정보를 가져올때 사용하는 HTTP 메서드, 데이터를 전송하면 쿼리파라미터를 통해 전송된다.(최근 body도 가능하다함)      
    *  조회를왜 GET으로? : 설계 원칙에 따라 GET 방식은 서버에게 여러 번 요청을 하더라도 동일한 응답이 돌아와야 한다.   
    *  캐시를 사용하는 걸로 알고 있다.   
* POST : 주로 정보를 갱신할 때 사용하는 HTTP 메서드, 데이터를 전송하면 HTTP 바디에 데이터를 넣어 전송한다.    

## 쿠키와 세션 
   
* 쿠키는 브라우저에 저장하고 매 요청시 데이터를 보내는 작업       
* 세션은 서버에 세션 스토리지를 만들고 세션ID에 따라 세션 스토리지에 접근해서 데이터를 제공하는 것     

### REST와 RESTful의 개념   
   
REAT 아키텍처를 모두 지킨 API를 원래는 REST API라 하는데 요즘 혼용이 많이되어서 RestFul API라고 한다.    

* client-server  
* stateless  
* cache  
* layer system   
* code-on-demand(optional)  
* **uniform interface**   

가장 중요한건 Uniform interface   

* 리소스로 식별 
* 메시지나 메타 데이터가 충분해야하고   
* HTTP 메시지 모든 요소에 대해서 해석이 가능해야하고  
* 하이퍼링크를 통해 상태가 전이될 수 있어야한다.  

## DNS 흐름 

1. 웹 URL에 링크를 치면, DNS에서 해당 URL을 IP포트로 찾아준다.   
2. 해당 IP포트를 이용하여 HTTP Message를 보낸다.  
3. 전송 프로토콜일 경우, 전송하기 전에 TCP 3 Way Handshake를 한다.  
4. 연결이 완료되면 데이터 전송을 시작한다.   
5. 

## CORS란?   
> Cross-Origin Resource Sharing 

![99033470-4b2a2800-25be-11eb-99ed-3964a246ff2e](https://user-images.githubusercontent.com/50267433/147178759-97f95429-eeff-408e-8d04-86b64ea0f374.png)

|protocol|Host|Port|Path|QueryString|Fragment|
|--------|----------|-----|-------|---------------------|-----|
|https://|github.com|:433/|kwj1270|?q=김우재 &sort=oldset|#foo|

    
* 출처를 판단하는 기준으로 `Protocol-Host-Port` 가 같다면 같은 출처라고 말을한다.      
* 단, Port는 브라우저마다 정책이 다르다.(IE에서는 포트 포함 안함)  
  
내가 가진 데이터를 다른 사람이 도난하는 것을 방지하고    
반대로, 다른 서버의 데이터를 가져와 내 서버를 망가뜨릴 수 있는걸 방지하기 위해  
