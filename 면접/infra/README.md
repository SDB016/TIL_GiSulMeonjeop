# VPC 
## 망분리 이유  



## AWS Private, Public subnet - VPC 설정 (NAT)
  
VPC내에는 보통 Public Subnet과 Private Subnet으로 구성되어 있다.     
  
* Public Subnet:     
    * Internet Gateway     
    * ELB   
    * Public IP/Elastic IP를 가진 인스턴스를 내부에 가지고 있다.    

* Private Subnet:    
    * 기본적으로 외부와 차단되어 있습니다. 
    * Private Subnet내의 인스턴스들은 private ip만을 가지고 있습니다.  
    * internet inbound/outbound가 불가능 하고 오직 다른 서브넷과의 연결만이 가능합니다.
    * 단, Public Subnet 내에 있는 Nat Instance를 통하여 인터넷이 가능해진다.   

## NAT   
공유기와 비슷, public network가 일종의 공유기 역할       
public network를 통해서 private network들이 인터넷을 사용하게끔 해준다.     
     
단, NAT 를 사용할때 단점은 여러명이 동시에 인터넷을 접속하게 되므로,        
실제로 접속하는 호스트 숫자에 따라서 접속 속도가 느려질 수 있다.        
다만 성능이 좋을수록 대역폭만 줄어들고 체감되는 속도저하는 꽤 적은편.      

## Route Table   

   
## CI/CD Blue, Green 아세요?


# EC2 
3 Tier VPC 사용경험 잇음 

# CloudWatch  
   
사용법에 대해서 공부를 했다.        
지하철 노선도의 최단 경로를 구하는 로직이 있는데 시간이 얼마나 걸리는지 측정을 했다.   
일반적으로 CPU사용량, 메모리, 네트워크 상태등에 대해서 모니터링 시켜보았다.  

