# TCP와 HTTP   
현시점에서 HTTP를 사용한다는 의미는 대개 TCP 기반의 HTTP 통신을 사용한다는 것과 같은 의미이다.      
즉, TCP로 연결을 주고 받다보니까 HTTP는 자연스레 TCP의 영향을 받고 있다는 뜻이기도 하다.     

TCP는 신뢰성을 높이기 위한 여러 작업들을 처리한다.(흐름 제어, 혼잡 제어, 에러 제어)      
그러나 이러한 TCP의 특성과 HTTP가 호환되지 않는 경우가 있었다.       
         
대표적인 예로 슬로우 스타터가 있는데           
과거 HTTP 1.0은 매 요청마다 커넥션을 연결하고 끊는 과정을 반복하는데          
슬로우 스타터는 커넥션을 새로 연결할 때 마다 시작한다.      
즉, 매 요청시 적은량의 패킷 사이즈를 보낼 수 밖에 없었다.      

이러한 관점에서 HTTP의 버전업에 대해서 살펴보자  

```
슬로우 스타터는 패킷의 사이즈를 점차 늘리면서 보내다가      
로스(패킷 손실)가 일어나면, 네트워크 혼잡으로 판단하고 window size 방식을 진행        
즉, 패킷의 양을 점점 늘리면서 최대한 패킷을 많이 보내려 하다가 문제 생기면 적정 수치부터 다시 진행  
그리고 이러한 슬로우 스타터는 TCP 커넥션을 시작할 때 마다 새로 시작한다.    
```  

# 📄 HTTP 1.0   
 
HTTP 1.0은 단순하게 open/operation/close의 방식을 취하고 있어서 단순하다.            
TCP connection당 하나의 URL만 fetch하며 매번의 `request`, `response`가 끝나면 연결을 끊는다.           

![image](https://user-images.githubusercontent.com/50267433/138400458-93c5d283-7dbe-459c-81a5-71f777a2ec6c.png)
         
**Http1.0은 필요할 때 마다 커넥션을 해야 하므로 속도가 떨어지며 TCP Slow Starter와 상성은 정말 최악이다.**           
Slow Starter는 커넥션이 생성될때 시작되며 초기에는 매우 낮은량의 패킷을 보낸다.                        
Http 1.0 같은 경우 매 요청시 새로 커넥션을 생성하기에 **매번 낮은량의 패킷을 보내게 되면서 성능상 이슈가 있다.**                      
   
* 커넥션 과정 및 비용으로 인한 성능 저하        
* Slow Starter 로 인한 성능 저하(적은량 패킷으로 초기화)    
      
이외에도 여러 다른 이유들로 인해, HTTP 1.1이 등장한다.       
     
# HTTP 1.1
     
![2638A3415828845026](https://user-images.githubusercontent.com/50267433/138406967-4371f9ab-0b06-483f-b79f-4aac5f3f2b27.png)   
             
HTTP 1.1에는 **keep-alive**라는 지속 커넥션을 이용하여 TCP Connection 비용을 대폭 줄였다.         
또한, 여러 요청을 입력받고 응답을 보내주는 **Pipelining**을 도입했다.       
                 
## keep-alive    
1. timeout 시간이 지나면 확인 패킷을 보낸다.      
    1. 응답을 받으면 다시 카운트 한다.            
    2. 응답을 받지 못하면 인터벌 타임 이후 다시 요청을 보내본다.(요청 횟수는 서버에서 설정 가능하다.)           
        1. 만약 여기서도 응답이 없다면 소켓을 닫아버린다.       
2. 소켓은 양측의 포트를 열고 통신하는 파이프라인 같은 것                 
    * 여기서 중요한 것은 **소켓 연결 == 포트를 여는 것 == 포트 없음 == 리소스 고갈**              
    * 즉, 웹 애플리케이션에서 설정된 기간까지 최대한 연결을 유지하려고 한다.      
                   
## Pipelining 과 HOL 블록킹 문제  
             
요청이 오면 응답을 넘겨주기까지 시간이 오래 걸린다.              
이로 인해, 다음 요청을 보내기까지 시간이 오래 걸린다는 몬제가 있었다.       
이를 해결하기 위해 **서버 쪽에서 Queue를 사용하여 처리하자는 생각에 Pipelining**이 도입되었다.             
   
![pipelining](https://user-images.githubusercontent.com/50267433/138417589-8e0ae007-74c4-4941-ab6b-391d53735381.jpg)
         
파이프라이닝은 한번에 여러 Request를 보내고 한번에 여러 response를 반환하는 것을 말한다.          
하지만, 여전히 **처음 요청이 처음 응답으로 반환해야하듯이 요청/응답에 순서를 보장해야한다는 문제가 있었다.**           
   
만약, 처음 요청에 대해서 서버가 처리하지 못한다면?       
나머지는 요청들에 대해서 blocking이 이루어지는 **HOL 블록킹(head of line blocking) 발생**           
        
## HOL 블록킹을 해결하기 위한 Multiple Connections    
![multiple](https://user-images.githubusercontent.com/50267433/138416897-44c0b985-d60e-4465-a019-cdb2ab313109.jpg)   
             
HOL(head of line) blocking 을 해결하기 위해서 **Multiple Connections이 도입되었다.**       
애초에 TCP 커넥션을 여러개 생성해서 **Request 요청을 병렬로 처리한다는 것이다**       
  
* A Conncetion: 1번 요청
* B Conncetion: 2번 요청
     
그러나 네트워크에도 통신되는 데이터 허용치 즉, 대역폭이 존재하는데               
대역폭을 너무 많이 차지하면서 오히려 Latency가 증가할 수 있다.                  
즉, 많은 데이터를 한번에 보내니까 부하를 발생시킬 수 있는 것이고 이로 인해 Latency가 증가될 수 있다.          
   
# HTTP 2.0  
  
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

