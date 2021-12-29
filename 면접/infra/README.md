# VPC   

# AWS VPC  
   
* 서브넷 : VPC에 설정한 네트워크 대역을 더 세부적으로 나눈 네트워크   
* 라우팅테이블 : 네트워크 트래픽을 전달할 위치를 결정하는 데 사용하는 라우팅이라는 이름의 규칙 집합    
* 인터넷 게이트웨이 : VPC의 리소스와 인터넷 간의 통신을 활성화하기 위해 VPC에 연결하는 게이트웨이   

## 서브네팅
## 라우팅 테이블   
   
## Internet GateWay     
VPC의 인스턴스와 인터넷 간에 통신할 수 있게 해준다.     
           
* 인터넷 라우팅 가능 트래픽에 대한 VPC 라우팅 테이블에 대상을 제공         
* 퍼블릭 IPv4 주소가 할당된 인스턴스에 대해 NAT(네트워크 주소 변환)를 수행하는 두 가지 목적이 있습니다.       
* 인터넷 게이트웨이 자세한 설명 클릭 -> [AWS document](https://docs.aws.amazon.com/ko_kr/vpc/latest/userguide/VPC_Internet_Gateway.html)        
       
인터넷 게이트웨이 + VPC 연결 -> VPC 인스턴스들이 인터넷에 접속 가능해진다.       
           
서브넷에 속한 EC2가 외부와 통신을 하기 위해서는       
자신의 라우팅 테이블에 설정된 정보를 제외한 모든 대역(0.0.0.0/0)에 대한 통신을 Internet Gateway로 요청하게끔 설정해두어야 합니다.      
라우팅 테이블을 생성하고 0.0.0.0/0 대역을 앞에서 생성한 Internet Gateway로 매핑합니다.     

## AWS Private, Public subnet - VPC 설정 (NAT)
  
VPC내에는 보통 Public Subnet과 Private Subnet으로 구성되어 있다.     
  
<img width="619" alt="b3c9ac82a4e94f2d95e1db822716408c" src="https://user-images.githubusercontent.com/50267433/147627981-099fd924-47f8-4f81-b945-4c8966cdc31b.png">            

* Public Subnet                
    * Internet Gateway                  
    * ELB            
    * Public IP/Elastic IP를 가진 인스턴스를 내부에 가지고 있다.                 
* Private Subnet            
    * 기본적으로 외부와 차단되어 있습니다.     
    * Private Subnet내의 인스턴스들은 private ip만을 가지고 있습니다.      
    * internet inbound/outbound가 불가능 하고 오직 다른 서브넷과의 연결만이 가능합니다.      
    * 단, Public Subnet 내에 있는 Nat Instance를 통하여 인터넷이 가능해진다.     
    
## NAT     
공유기와 비슷, public network가 일종의 공유기 역할     
public network를 통해서 private network들이 인터넷을 사용하게끔 만든다.        
          
단, NAT 를 사용할때 단점은 여러명이 동시에 인터넷을 접속하게 되므로             
실제로 **접속하는 호스트 숫자에 따라서 접속 속도가 느려질 수 있다.**              
다만 성능이 좋을수록 대역폭만 줄어들고 체감되는 속도 저하는 꽤 적은편.         
   
## Route Table   

![image](https://user-images.githubusercontent.com/50267433/147628128-54555475-ed4d-4ee5-b0dd-95d8a761acf2.png)    
   
**서로 다른 네트워크간의 통신을 중계**     
* MAC 테이블에 정보가 있을 때 : Forwarding      
* MAC 테이블에 정보가 없을 때 : Drop     
* 라우팅 프로토콜을 활용하여       
          
어떤 대역으로 패킷을 보내는 것이 최적 경로인지 학습      
    
* 외부 네트워크와 통신하기 위해서는 Public IP가 있어야 함     
* 라우터는 Private IP가 목적지일 경우 인터넷 구간으로 보내지 않음     
* 따라서, Private IP를 Public IP로 변환해주어야 함(NAT)      

* 자신이 속한 subnet(172.16.0.0/24)의 서버는 가상 스위치를 통해 직접 통신
* 자신이 속하지 않은 subnet(172.16.1.0/24)은 가상 라우터를 통해 직접 통신
* 그 외의 0.0.0.0/0 (전체 대역)은 Internet Gateway로 통신을 보내도록 학습
  

## CI/CD Blue, Green 아세요?


# EC2 
3 Tier VPC 사용경험 잇음 

# CloudWatch  
   
사용법에 대해서 공부를 했다.        
지하철 노선도의 최단 경로를 구하는 로직이 있는데 시간이 얼마나 걸리는지 측정을 했다.   
일반적으로 CPU사용량, 메모리, 네트워크 상태등에 대해서 모니터링 시켜보았다.  

