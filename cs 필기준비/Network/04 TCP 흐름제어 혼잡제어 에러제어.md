# 흐름제어 
> 송신측과 수신측의 데이터 처리 속도 차이를 해결하기 위한 기법   
    
**TCP Buffer**   
* 송신자 : 버퍼에 세그먼트를 보관하고 이후 순차적으로 전송한다.     
* 수신자 : 응용프로그램이 세그먼트를 읽을때까지 버퍼에 저장한다.    
     
**TCP Window Size**        
* Window Size == 수신 TCP Buffer 크기      
* 송신측에서 보내는 데이터가 버퍼를 넘지 않도록 사이즈를 조절하는 것이다.       
    * 송신측은 ACK를 수신하기 전까지 윈도우 크기 만큼의 세그먼트를 연속해서 전송할 수 있다.       
    * 송신측이 ACK를 수신하면 다시 보낼 수 있는 세그먼트의 수 만큼 윈도우 사이즈를 조절한다.     
    * 윈도우 크기가 0이되면, 더이상 전송을 하지 못하고 ACK를 받을 때까지 대기한다.         

**재전송**   
* TCP는 ACK를 수신하지 못할 경우 무한정 기다리는 것을 피하기 위해    
  일정시간이 지나면(time_out) 재전송을 한다.    
* 단, 버퍼가 차서 못보내는 것이라면 상황을 더 악화시키는 것이기도 하다.  
             
**수신측의 버퍼크기를 어떻게 전송하고 있는 것일까? 🤔**         
* 수신 TCP는 현재의 남아있는 버퍼 크기를 **ACK로 전송할 때 window size 필드를 통해서 알려준다.**        
      
# 혼잡제어   
> 망에 입력되는 트래픽 양이 망이 처리할 수 있는 한도를 초과할 경우 체증이 발생한다.    

* 패킷망에서는 트래픽의 흐름은 일정하지 않다.(회선망과의 차이점)           
* 망의 트래픽 처리 용량을 최대 트래픽 전송율보다 크게 유지할 수 있으면 체증을 피할 수 있다.   
* Congestion(혼잡)은 패킷망에서 해결해야 할 가장 중요한 과제이자 가장 어려운 과정 중 하나이다.         

입력되는 패킷의 수가 많아질 수록 처리해야할 양이 많아지는 것은 당연하며,      
패킷의 수가 증가할수록 딜레이가 되는 비율은 기하급수적으로 증가되는 형태를 보인다.    
   
이러한 혼잡 제어를 해결하기 위해서는 2가지 제어 방식이 존재한다.   

1. 예벙적 체증 제어 
2. 반응적 체증 제어   

**예방적 체증제어** 
* 사전에 망에 입력되는 트래픽양을 조절하는 기법이다.     
* 2단계로 이루어진다.      
    1. 망사용자와 사용자가 계약하여, 사전에 전송할 데이터양을 정한다(call admission control)  
    2. 망사업자는 사용자가 사전에 약속된 내용을 준수하는지 감시한다.(policing)   
* 라우터에 패킷을 전송할 때, 사전에 약속된 계약에 따라 패킷의 전송 순위를 결정한다.(priority control)     
      
**반응적 체증제어**           
* 체증현상이 발생할 때 트래픽양을 감소시킨다.(줄이라고 통보)            
* 패킷의 지연시간(증가되는지), 라우터의 버퍼 길이 등을 계속 측정하면서 혼잡 상태를 초기에 발견한다.             
* 반응적 체증 제어를 수행하기에 적합한 계층은 사실 네트워크 계층이며 라우터가 적당하다.(모니터링 및 전송량이므로)         
* 하지만, 인터넷 프로토콜에서는 체증 제어의 임무를 TCP가 수행하도록 하고 있다.   

## TCP의 혼잡제어   
  
**혼잡 발견(Congestion Detection)**      
* TCP는 송신한 패킷에 대해서 ACK를 수신한다.  
* 만약 정해진 시간(time_out)이 지날 때까지 ACK이 도착하지 않으면 Congestion이 발생한 것으로 판단한다. 
* 흐름제어와 유사한데, 사실 혼잡제어와 흐름제어를 별개로 볼게 아니라 흐름제어를 기본으로 진행한다고 이해하자     

**혼잡 제어(Congestion Control) 2가지 대응**        
* Slow Start : 
    * TCP 호스트(송신측)은 처음에는 적은 양의 패킷을 전송하고 점차 양을 늘려나간다.       
    * Congestion 발생과 time out과 상관없이 모든 TCP 호스트(송신측)는 Slow Start로 패킷을 보낸다.      
* Congestion Avodiance : 
    * Congestion 발생으로 판단되면(time_out), 전송되는 패킷의 양을 초기 상태로 줄여서 다시 시작한다.   
   
**Congestion Control의 2개의 Window**     

* Awnd(advertised window)   
    * 초기 연결 설정 단계에서, TCP는 상대 TCP에게 자신의 최대 버퍼크기(초기 Awnd)를 알려준다.        
    * 세그먼트를 수신할 때마다 TCP는 현재 자신의 버퍼 중 비어있는 공간의 크기(Awnd)를 알려준다.      
    * 이것은 TCP 흐름제어에서도 언급하는 window size이다.     
* Cwnd(congestion window)     
    * TCP가 세그먼트를 전송할 때 ACK을 받지않고 연속해서 보낼 수 있는 세그먼트의 양을 결정한다.         
    * 즉, TCP 흐름제어에 의하면 Tcp는 Awnd 만큼 연속해서 세그먼트를 전송할 수 있다.          
    * 하지만 **Congestion Control에 의해서 Awnd만큼 전송할 수 없고 Cwnd만큼 전송하게 된다.**         

## Slow Start 

![image](https://user-images.githubusercontent.com/50267433/146672173-78624a16-f07a-4cd3-9f86-bfab612dccc7.png)

```
Cwnd = Cwnd + 1 until min(Cwnd, Awnd)  
```

처음에는 1을 보내고, ACK을 받으면 Cwnd를 1 늘리고 개수를 증가시키고 다시 전송한다.        
즉, 1씩 계속 증가하다가 그 혼잡이 탐지되면 다시 그 값을 줄이고 보내는 작업을 반복한다.(증가률 다시)       

## Congestion Avoidance 

* TCP는 timeout 될때까지 ACK를 받지 못하면 
  congestion이 발생한 것으로 판단하고, congestion avoidance를 수행한다.  
* 즉, 전송률을 감소시킨다.   

**Congestion Avoidance algorithm**
1. timeout이 발생할때 까지, Cwnd를 1씩 증가하면서 데이터를 전송한다.  
2. timeout이 발생하면, Awnd 의 1/2 만큼의 위체에 threshold를 설정하고 cwnd를 1로 맞춘다.   
3. Cwnd가 threshold 까지 증가하다가 이를 넘어가버리면 다시 1씩 증가된다.(증가률 다시 봐야할듯) 

![image](https://user-images.githubusercontent.com/50267433/146672387-6064991d-0b83-4748-9271-40ce043a95c1.png)


## Fast Retransmit 와 Fast Recovery   
  
**동일한 ACK를 3개 받을 경우**     
* 동일한 ACK가 계속 도착한다는 것은 Congestion 으로 판단하지만,  
  그렇더라도 상태가 심각하지 않다고 해석할 수 있다.   
* 그래서 Congestion Avoidance 보다는 좀더 적극적으로 전송한다.    
  
**Fast Retransmit**     
* time out 되기전에 바로 재전송한다.   

**Fast Recovery**   
* Cwnd를 현재의 Cwnd의 반으로 줄인다.     
* 그리고 줄인 Cwnd에서부터 Linear 하게 증가시킨다.   
 
![image](https://user-images.githubusercontent.com/50267433/146672505-6f3aaa88-99db-4060-9cec-a87a2e58a0db.png)
   
![image](https://user-images.githubusercontent.com/50267433/146672517-7c8e2a44-fa5f-4973-b9ac-e7665ce83d1c.png)
   
    
# 오류제어 

https://www.youtube.com/watch?v=FxDRd71xfpw&ab_channel=%EC%9D%B4%EC%82%B0%EC%88%98%ED%95%99   
 
* 시퀀스넘버 기반
* ACK로 수신 확인
* 오류 발생 시 CRC이용, 송신측에 프레임 재전송 요청
