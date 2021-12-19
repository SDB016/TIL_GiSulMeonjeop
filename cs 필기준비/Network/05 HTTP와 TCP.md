        1. 만약 여기서도 응답이 없다면 소켓을 닫아버린다.      
2. 소켓은 양층의 포트를 열고 통신하는 파이프라인 같은 것              
   여기서 중요한 것은 **소켓 연결 == 포트를 여는 것 == 포트 없음 == 리소스 고갈**             
   즉, 웹 애플리케이션에서 설정된 기간까지 최대한 연결을 유지하려고 한다.          
      
## pipelining 과 HOL 블록킹
**서버 쪽으로 Queue를 넘겨 FIFO로 처리하면 안되나? 라는 생각에 도입**    

![pipelining](https://user-images.githubusercontent.com/50267433/138417589-8e0ae007-74c4-4941-ab6b-391d53735381.jpg)

파이프라이닝은 한번에 여러 Reqeust를 한번에 보내고 한번에 여러 response를 받는 것을 말한다.       
하지만, 여전히 처음 요청이 처음 응답으로 와야 되듯이 요청/응답에 순서를 보장해야한다는 문제가 있었다.     
만약, 처음 요청에 대해서 서버가 처리하지 못한다면?       
나머지는 요청들에 대해서 blocking이 이루어지는 **HOL 블록킹(head of line blocking) 발생**           
      
## Multiple Connections    
![multiple](https://user-images.githubusercontent.com/50267433/138416897-44c0b985-d60e-4465-a019-cdb2ab313109.jpg)   
       
head of line blocking 을 해결하기 위해서 Multiple Connections이 도입되었다.    
애초에 TCP 커넥션을 여러개 생성해서 Request 요청을 병렬로 처리한다는 것이다    

* A Conncetion: 1번 요청
* B Conncetion: 2번 요청

그러나 네트워크에도 통신되는 데이터 허용치 즉, 대역폭이 존재하는데          
대역폭을 너무 많이 차지하면서 오히려 Latency가 증가할 수 있다.            
즉, 많은 데이터를 한번에 보내니까 부하를 발생시킬 수 있는 것이고 이로 인해 Latency가 증가될 수 있다.        
   
# HTTP 2.0  
HTTP 1.1을 해결하고자 나온게 바로 HTTP 2.0   
  
![슬라이드1](https://user-images.githubusercontent.com/50267433/138418948-144409d4-6eb0-4e31-8660-e904fda12806.PNG)

* Steam은 여러 message들로 구성 되어있다.
* message는 header/data등의 frame으로 구성 되어있다.
* stream에는 식별자를 붙인다.
* 요청 응답 순서에 상관없이 전달 받더라도 서버 응답이 비동기 방식으로 처리된다
  

쉽게 설명하자면, HttpMessage에 존재하는 header 와 body를 header frame 과 data frame이라는 형태로 래핑을 한다.   
그리고 헤더/데이터 프레임을 메시지라 부르고 이 여러 메시지들이 스트림으로 구성되어 있다.       

![image (2)](https://user-images.githubusercontent.com/50267433/138419294-2cfec1b6-f8c8-4f40-b9ed-75f5ecb130e5.png)
    
각각의 스트림들은 식별자를 가지고 있으므로 병렬 생성하여 사용할 수 있다.      
즉, 식별자로 각각의 스트림 찾아서 로직 결과를 담으면 되니까 응답 순서에 상관이 없다.           
이는 곧, 하나의 TCP 연결을 통해 다수의 클라이언트 요청 처리가 가능해졌다는 것을 의미한다.     

## Multiplexing 

![Comparison-of-HTTP-versions](https://user-images.githubusercontent.com/50267433/138419777-7506a97c-287c-4be8-9f60-fb5cdb51767d.png)
   
응답에 관하여 논블락킹으로 처리할 수 있으므로 응답 순서에 상관이 없다.        

