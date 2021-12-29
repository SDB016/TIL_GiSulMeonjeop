# VPC 
## 망 분리 이유  



## 망
  
* 망 : 노드들과 이들 노드들을 연결하는 링크들로 구성된 하나의 시스템    
* 노드 : IP로 식별할 수 있는 대상         
* 링크 : 물리적 회선         
     
즉, 하나의 Subnet을 하나의 망이라고 칭할 수 있겠네요        
      
* Region : 국가 / 지역       
* Availability Zone : 데이터센터       
    * ap-northeast-2a      
    * ap-northeast-2b       
* VPC          
    * 하나의 Region에 종속       
    * 다수의 AZ 설정 가능          
    * VPC IP 대역 내에서 망 구성         

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

## Internet GateWay 
VPC의 인스턴스와 인터넷 간에 통신할 수 있게 해준다.   
        
* 인터넷 라우팅 가능 트래픽에 대한 VPC 라우팅 테이블에 대상을 제공        
* 퍼블릭 IPv4 주소가 할당된 인스턴스에 대해 NAT(네트워크 주소 변환)를 수행하는 두 가지 목적이 있습니다.     
* 인터넷 게이트웨이 자세한 설명 클릭 -> [AWS document](https://docs.aws.amazon.com/ko_kr/vpc/latest/userguide/VPC_Internet_Gateway.html)      

  
인터넷 게이트웨이 + VPC 연결 -> VPC 인스턴스들이 인터넷에 접속 가능해진다.  




## Bastion       
     
22번 포트의 경우 보안이 뚫린다면 서비스에 심각한 문제를 일으킬 수 있다.        
그렇다고 모든 서버들에 보안 수준을 높게 잡으면, Auto-Scaling 등 확장성을 고려한 구성과 배치된다.               
이 경우 관리 포인트가 늘어나기에 **일반적으로는 보안 설정을 일정 부분을 포기하는 결정을 하게 된다.**        

Bastion 이란, 성 외곽을 보호하기 위해 돌출된 부분으로 적으로부터 효과적으로 방어하기 위한 수단이다.  
즉, 22번 포트로 접근 가능한 서버를 Bastion Server로 한정 짓고 Bastion server 에서 다른 vpc 서버로 이동하는 방식을 사용한다면   
악성 루트킷, 랜섬웨어 등으로 피해를 보더라도 Bastion Server만 재구성하면 되므로, 서비스에 영향을 최소화할 수 있다.         
             
추가적으로, **서비스 정상 트래픽과 관리자용 트래픽을 구분할 수 있다는 이점이 있다.**                  
가령, **서비스가 DDos 공격을 받아 대역폭을 모두 차지하고 있다면**      
**일반적인 방법으로 서비스용 서버에 접속하기는 어렵기 때문에 별도의 경로를 확보해둘 필요가 있다.**        
         
Bastion -> Public -> Private 이러한 방식을 3-Tier-Architecture 라고 부른다.      
   
## CI/CD Blue, Green 아세요?


# EC2 
3 Tier VPC 사용경험 잇음 

# CloudWatch  
   
사용법에 대해서 공부를 했다.        
지하철 노선도의 최단 경로를 구하는 로직이 있는데 시간이 얼마나 걸리는지 측정을 했다.   
일반적으로 CPU사용량, 메모리, 네트워크 상태등에 대해서 모니터링 시켜보았다.  

