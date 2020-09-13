# Part 1-3 Network

* [HTTP 의 GET 과 POST 비교](#http의-get과-post-비교)
* [TCP 3-way-handshake](#tcp-3-way-handshake)
* [TCP와 UDP의 비교](#tcp와-udp의-비교)
* [HTTP 와 HTTPS](#http와-https)
  * HTTP 의 문제점들
* [DNS Round Robin 방식](#dns-round-robin-방식)
* [웹 통신의 큰 흐름](#웹-통신의-큰-흐름)

[뒤로](https://github.com/JaeYeopHan/for_beginner)

</br>

## HTTP의 GET과 POST 비교

공통점 : HTTP 프로토콜을 이용해서 서버에 무엇인가를 요청할 때 사용하는 방식이다. 

### GET

GET 방식 : 요청하는 데이터가 `HTTP Request Message`의 **Header** 부분의 url 에 담겨서 전송된다.      
url 상에 `?` 뒤에 데이터가 붙기 때문에 전송할 수 있는 데이터의 크기가 제한적이다.           
또 보안이 필요한 데이터에 대해서는 데이터가 그대로 url 에 노출되므로 `GET`방식은 적절하지 않다.            
    
### POST
     
POST 방식의 request 는 `HTTP Message`의 **Body** 부분에 데이터가 담겨서 전송된다.        
데이터 크기가 GET 방식보다 크고 보안면에서 낫다.         

_그렇다면 이러한 특성을 이해한 뒤에는 어디에 적용되는지를 알아봐야 그 차이를 극명하게 이해할 수 있다._    
GET 은 가져오는 것이다.    
서버에서 어떤 데이터를 가져와서 보여준다거나 하는 용도이지 서버의 값이나 상태 등을 변경하지 않는다.     
SELECT 적인 성향을 갖고 있다고 볼 수 있는 것이다.    
    
POST 는 서버의 값이나 상태를 변경하기 위해서 또는 추가하기 위해서 사용된다.     
     
[뒤로](https://github.com/JaeYeopHan/for_beginner)/[위로](#part-1-3-network)

</br>

## TCP 3-way Handshake
     
1. 클라이언트 -> 서버 : **연결 요청 패킷** SYN(a) 전송          
2. 서버 -> 클라이언트 : SYN(a) 받고, **연결 요청 응답 패킷** ACK(a+1)와 SYN(b) **연결 요청 패킷** 전송          
3. 클라이언트 -> 서버 : ACK(a+1)와 SYN(b) 받고, **연결 요청 응답 패킷** ACK(b+1) 을 전속하면 연결이 성립됩니다.         
       
___        
           
1. 너 내 말 들리니 syn    
2. 응 들려 ack 너도 내말 들리니 syn    
3. 응 들려 ack    
  
## TCP 4-way Handshake    
   
1. 클라이언트 -> 서버 : 연결 종료를 의미하는 **FIN 플래그** 전송        
2. 서버 -> 클라이언트 : FIN 플래그 받고 **확인 패킷 ACK 전송**        
3. 그리고 데이터를 모두 보낼때까지 잠깐 TIME_OUT      
4. 서버 -> 클라이언트 : 데이터 모두 보내고 통신이 끝났으면 연결 종료 **FIN 플래그** 전송     
5. 클라이언트 -> 서버 : FIN 메시지 확인후 **확인 패킷 ACK 전송**      
      
* 서버 : 클라이언트의 ACK를 받으면 **소켓 연결 CLOSE**          
* 클라이언트 : 서버로부터 아직 받지 못한 데이터 대비해 일정시간 동안 대기 TIME_OUT         
         
[뒤로](https://github.com/JaeYeopHan/for_beginner)/[위로](#part-1-3-network)

</br>

## TCP와 UDP의 비교

### UDP

`UDP(User Datagram Protocol, 사용자 데이터그램 프로토콜)`    
* **비연결형 전송 프로토콜** 로서 속도가 빠르나 신뢰성과 안정성을 보장해주지는 않는다. (재전송 x)    
    
`UDP`를 사용한 것들에는 `DNS`가 있다.      
사전에 설정이 필요하지 않으며 그 후에 해제가 필요하지 않다.     
    
</br>

### TCP

`TCP(Transmission Control Protocol, 전송제어 프로토콜)` :   
* **연결형 전송 프로토콜**로서 신뢰성 과 안정성을 보장해준다.     
* TCP 서비스는 송신자와 수신자 모두가 소켓이라고 부르는 종단점을 생성함으로써 이루어진다. -> 가상 회선      
* TCP 에서 연결 설정(connection establishment)는 `3-way handshake`를 통해 행해진다.     
     
모든 TCP 연결은 전이중(full-duplex), 점대점(point to point)방식이다.           
전송이 양방향으로 동시에 일어나며 각 연결이 정확히 2 개의 종단점을 가지고 있다.                  
    
TCP 는 멀티캐스팅이나 브로드캐스팅을 지원하지 않는다.         

#### Reference

* http://d2.naver.com/helloworld/47667
* http://asfirstalways.tistory.com/327

[뒤로](https://github.com/JaeYeopHan/for_beginner)/[위로](#part-1-3-network)

</br>

## HTTP와 HTTPS

### HTTP 의 문제점

* HTTP 는 평문 통신이기 때문에 **도청**이 가능하다.
* 통신 상대를 확인하지 않기 때문에 **위장**이 가능하다.
* 완전성을 증명할 수 없기 때문에 **변조**가 가능하다.

_위 세 가지는 다른 암호화하지 않은 프로토콜에도 공통되는 문제점들이다._
       
#### 보완 방법
     
`HTTPS`를 사용해야 한다. SSL 에는 수신자 인증이나 암호화, 그리고 다이제스트 기능을 제공하고 있다.      
       
</br>  

### HTTPS
    
> HTTP 에 암호화와 인증, 그리고 완전성 보호를 더한 HTTPS       
            
`HTTPS`는          
HTTP 통신시 소켓 부분을 `SSL` or `TLS`라는 프로토콜로 대체하는 것 뿐이다.       
              
HTTP 는 원래 TCP 와 직접 통신했지만,           
HTTPS 에서 HTTP 는 SSL 과 통신하고 **SSL 이 TCP 와 통신** 하게 된다.           
SSL 을 사용한 HTTPS 는 암호화와 증명서, 안전성 보호를 이용할 수 있게 된다.         
        
HTTPS 의 SSL 에서는 공통키 암호화 방식과 공개키 암호화 방식을 혼합한 **하이브리드 암호 시스템**을 사용한다.       
공통키를 공개키 암호화 방식으로 교환한 다음에 다음부터의 통신은 공통키 암호를 사용하는 방식이다   .          
            
#### 모든 웹 페이지에서 HTTPS 를 사용하지 않는 이유
         
암호화 통신은 CPU 나 메모리 등 리소스가 많이 필요하다.                   
통신할 때마다 암호화를 하면 많은 리소스를 소비하기 때문에 서버 한 대당 처리할 수 있는 리퀘스트의 수가 줄어들게 된다.          
그렇기 때문에 민감한 정보를 다룰 때만 HTTPS 에 의한 암호화 통신을 사용한다.             
       
_cf) HTTP 2.0 이 발전되면서 HTTPS 가 HTTP 보다 빠르다는 사실이 나왔는데요, 다음 링크를 통해 보다 자세한 내용을 확인하실 수 있습니다._    
관련 링크 : [HTTPS 가 HTTP 보다 빠르다.](https://tech.ssut.me/https-is-faster-than-http/)      
      
[뒤로](https://github.com/JaeYeopHan/for_beginner)/[위로](#part-1-3-network)  
    
</br>

## DNS round robin 방식    
라운드로빈 : 프로세스들 사이에 우선순위를 두지 않고,           
순서대로 시간단위(Time Quantum/Slice)로 CPU를 할당하는 방식의 CPU 스케줄링 알고리즘입니다.               
DNS 라운드 로빈 : Domain에 대한 IP 요청 쿼리 시, Round-Robin으로 IP를 반환하는 방식                 
    
1. 유저는 DNS 서버에서 Domain Name을 이용하여, IP를 얻어옴    
2. Domain Name Server는 접속하는 유저에 대해 Round Robin 식으로 IP를 할당함    
    
_Round Robin 방식을 기반으로 단점을 해소하는 DNS 스케줄링 알고리즘이 존재한다. (일부만 소개)_
     
#### Weighted round robin (WRR)
       
각각의 웹 서버에 가중치를 가미해서 분산 비율을 변경한다.        
물론 가중치가 큰 서버일수록 빈번하게 선택되므로 처리능력이 높은 서버는 가중치를 높게 설정하는 것이 좋다.        

#### Least connection   
     
접속 클라이언트 수가 가장 적은 서버를 선택한다.     

</br>

[뒤로](https://github.com/JaeYeopHan/for_beginner)/[위로](#part-1-3-network)

</br>

# 트래픽이 많을 경우 어떻게 처리할 것이냐  
1. 로드밸런싱(Load Balancing)       
- 트래픽이 많을 때 여러 대의 서버가 분산처리하여 서버의 로드율을 증가, 부하량, 속도저하등 고려하여 분산처리하여 해결해주는 서비스         
- 단 DB는 동일한 DB를 사용    
2. RDBMS 사용할 경우 파티셔닝 작업 테이블을 수직, 수평으로 파티셔닝  
3. write back 기법 사용 -> cpu cache에 저장했다가 후에 데이터베이스를 갱신  
4. 디스크기반 데이터베이스 대신 메모리 기반의 DB를 사용하는 것       
- 저장 용량이 커질 수록 접근 속도에서 차이가 난다.      
- redis 같은 경우 cahce에 데이터를 저장했다가 후에 데이터 베이스를 갱신   


_Network.end_
