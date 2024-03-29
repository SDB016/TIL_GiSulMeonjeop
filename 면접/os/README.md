# 프로세스와 스레드  

## 운영체제란?  

사용자와 소프트웨어 사이에서 인터페이스 역할을 하는 소프트웨어 

## 프로세스란? 
메모리에 올라와 실행되고 있는 프로그램의 인스턴스     

* 운영체제는 프로세스마다 독립적인 메모리를 할당해준다.         
* 프로세스들은 독립적이기 때문에 통신하기 위해 IPC를 사용해야 한다.
* 프로세스는 최소 1개의 쓰레드(메인 쓰레드)를 가지고 있다   
   
## 스레드란?   
프로세스 내에서 할당받은 자원을 이용해 동작하는 실행 단위        
     
* 쓰레드는 Stack과 PC Register를 제외한, Code/Data/Heap 영역을 공유한다.       
* Stack을 독립적으로 할당하는 이유는          
  스레드마다 독립적인 함수 호출, 실행을 하기 위해서 독립적으로 할당한다.
  만약 공유할 경우 LIFO 순서가 뒤틀릴 수 있다.   
* PC Register 를 독립적으로 할당하는 이유는  
  컨텍스트 스위칭이 발생했을 때 쓰레드의 상태 정보를 기억하고 다시 사용하기 위해서 독립적으로 할당한다.    
* 쓰레드는 프로세스의 자원을 공유하기 때문에 다른 쓰레드에 의한 결과를 즉시 확인할 수 있다.   
 
## 프로세스간 통신은?   

1. 공유 메모리 : 프로세스끼리 규약을 정하고 데이터를 공유하는 공간(동기화 신경써야함, 빠르다)   
    1. 공유 메모리 : 프로세스간 메모리 영역을 공유해서 사용할 수 있도록 허용    
    2. 메모리 맵 : 열린 파일을 메모리에 매핑   
2. 메시지 전달 시스템 : 메세지를 이용하여 통신한다. (다른 컴퓨터에도 통신가능, 느리다.)     
    1. 파이프 : 한쪽 방향으로만 통신이 가능한 반이중 통신(양방향 위해서2개 만듬, 단방향도 있음)        
    2. 소켓 : 양방향 통신이 가능한 기술로, 3way handshake로 연결 후 데이터 통신      
    3. 메시지큐 : 프로세스 중간에 존재하는 메모리 공간으로, 큐에 메시지를 보내고 이를 처리하는 기술       
 
## 프로세스와 스레드의 차이

* 멀티 프로세스 
    * 하나의 프로그램을 여러 개의 프로세스로 구성하여 각 프로세스가 1개의 작업을 처리하도록 하는 것
    * 특징
        * 1개의 프로세스가 죽어도 자식 프로세스 이외의 다른 프로세스들은 계속 실행된다.
        * Context Switching을 위한 오버헤드(캐시 초기화, 인터럽트 등)가 발생한다.
        * 프로세스는 각각 독립적인 메모리를 할당받았기 때문에 통신하는 것이 어렵다.
        
* 멀티 쓰레드
   * 하나의 프로그램을 여러 개의 쓰레드로 구성하여 각 쓰레드가 1개의 작업을 처리하도록 하는 것
   * 특징
       * 프로세스를 위해 자원을 할당하는 시스템콜이나 Context Switching의 오버헤드를 줄일 수 있다.
       * 쓰레드는 메모리를 공유하기 때문에, 통신이 쉽고 자원을 효율적으로 사용할 수 있다.
       * 하나의 쓰레드에 문제가 생기면 전체 프로세스가 영향을 받는다.
       * 여러 쓰레드가 하나의 자원에 동시에 접근하는 경우 자원 공유(동기화)의 문제가 발생할 수 있다.
       
## 멀티 스레드 이점과 문제점 

메모리를 공유한다는 차원에서 프로세스를 교체하지 않아도 되므로 컨텍스트 스위칭이 덜 발생하여 오베헤드가 적다.       
그리고 하나의 스레드가 갱신한 값을 다른 스레드가 바로 반영할 수 있다.         
단, 여러 스레드가 동시에 같은 메모리를 바라보고 있기에 RaceCondition이 발생할 수 있다.   
  
## RaceCondition이란?  

둘 이상의 쓰레드가 하나의 자원을 차지하기 위해 경쟁하는 것을 말한다.   

## RaceCondition 해결방법   

* 상호 배제 : 여러 스레드가 동시에 같은 리소스에 접근을 못하도록 한다.(스레드 갯수 제한 가능)  
* 점유 대기 : 스레드가 자원을 점유하면 작업을 마칠때까지 점유한 자원을 내놓지 않도록 한다.        
* 선점 불가 : 스레드가 다른 스레드로부터 자원을 빼앗지 못하도록 한다.          
* 순환 대기 : 스레드가 필요한 자원이 서로 다른 스레드에 있는 경우의 현상을 말한다.  
  
## DeadLock이란?   

서로 다른 스레드들이 서로가 원하는 자원을 가지고 있어서     
무한히 대기 상태에 이르는 것을 말한다.     

## DeadLock 해결 4가지 
 
1. 예방 : 상호배제, 점유 대기, 선점 불가, 순환 대기 중 한가지를 어긴다.     
2. 회피 : 은행원 알고리즘을 사용해서 문제를 해결한다.    
3. 탐지 및 복구 : 자원할당 그래프를 그려서 문제가 되는 영역을 찾아 진단하고 복구하는 작업    
4. 무시 : 말 그대로 무시하는 방법     
 
## 은행원 알고리즘 

쉽게 설명하면, 특정 고객에게 남은 돈을 다 대출해줬을때 상환이 가능한지 확인하는 알고리즘      
현재 은행에 남아있는 돈을 특정 고객에게 전부 대출해줄 경우 상환이 가능하면 안전상태, 아니면 비안전상태    

## 자원할당 그래프 
    
스레드와 각각의 필요한 자원들의 의존성을 그래프로 나타내어 판단하는 것      
  
# 프로세스 상태와 스케줄러   
## 프로세스 흐름 설명       
## 컨텍스트 스위칭    
    
CPU는 하나의 프로세스만 동작시킬 수 있기 때문에 프로세스가 교체를 하는 작업을 해야하는데 이를 컨테스트 스위칭이라한다.   

## 장기 스케줄러   

HDD에 있는 프로그램을 메모리에 올리는 작업  
Job Queue에 올린다.  
  
## 중기 스케줄러   
   
HDD와 메모리 사이에서 프로세스를 스와핑하는 것  
        
## 단기 스케줄러    
     
메모리에 올라와있는 프로세스를 ReadyQueue에 배치시키는 것  
  
## 단기 스케줄러 알고리즘 

* FCFS(First Come First Served) : 먼저들어오면 먼저처리    
* SJF(Shortest - Job - First) : 짧은 처리 순서가 우선순위(비선점)    
* SRT(Shortest Remaining time First) : 짧은 처리순서가 우선순위(선점)  
* Priority Scheduling : 특정 우선순위가 높은 프로세스먼저 처리, aging 기법으로 해결가능
* Round Robin : 특정 작업시간을 기준으로두고, 시간이 지나면 다시 대기하도록한다.  

# 가상 메모리   
  
모든 데이터를 올리지 않고, 일부만 올려서 작업을 처리하는 방법        
만약 필요한 페이지가 없다면 페이지 교체 알고리즘으로 해당 페이지를 가져와서 사용하고      
더 효율을 높이기 위해서 메모리 구석에 캐시 영역을 만들어서 캐시하면서 사용한다.  

## 페이지 교체 알고리즘
FIFO: 선입 선출 구조
LRU : 가장 사용되지 않은 페이지 삭제
LFU : 첨조 횟수가 가장 적은 페이지 삭제

## 페이징  
## 세그멘테이션  
## 내부 단편화 및 외부 단편화 설명   
## Page Fault 흐름 설명   
  
# Block VS Non Block VS Sync VS Async  
 
제어권 반환을 블락킹/논블락킹하냐의 차이      
프로그램의 시작과 끝을 동기화로 맞추냐 안맞추냐의 차이      

# 이외에도  
## 동시성과 병령성 차이 

동시성은 하나의 코어에서 다수의 작업을 처리하는 것으로, 사실상 동시는 아니지만 동시처럼 보이도록 작업한다.     
병렬성은 여러 코어에서 다수의 작업을 동시에 처리하는 것, 실제로 동시로 작업하는 것을 말한다.     

