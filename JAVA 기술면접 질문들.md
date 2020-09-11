# JVM구조에 대해 설명하시오.   
1. JAVA SOURCE : 사용자가 정의한 자바 파일 
2. COMPILER : 자바를 클래스 파일로 변환    
3. ByteCode : 클래스 파일들       
4. ClassLoader : 클래스 파일들을 JVM으로 로드 및 링크하여 RuntimeDataArea에 배치        
5. ExecutionEngine : 로딩된 클래스 파일들의 바이트 코드를 해석하여 JVM에서 실행가능하도록 한다.         
6. RuntimeDataArea : JVM이라는 프로세스가 프로그램을 수행하기 위하여 OS로부터 받은 메모리 공간      
    
**RuntimeDataArea** -> 메모리 구조      
* 메서드 영역 :        
클래스 정보를 처음 메모리 공간에 올릴때 **초기화되는 대상을 저장하기 위한 메모리 공간**        
클래스파일을 읽어서 분석하여 클래스에 대한 정보를 저장, 클래스 변수도 같이 저장      
    
* 힙 :     
인스턴스가 생성되는 공간, 인스턴스 변수들이 생성되는 공간    
     
* 스택 :     
메서드의 작업에 필요한 공간을 제공         
메서드가 호출되면 호출스택에서 준비한 메모리가 할당된다.            
메서드 작업 종료시 메모리 공간 반환되어 비워짐        


# GC처리 방법에 대해 설명하시오.
* 메모리가 부족할 때 사용되지 않는 메모리 즉, 쓰레기 메모리를 개발자가 해제하는 것이 아니라 JVM에서 해제해주는 것      
* 메모리 부족 요청시 실행 또는 JVM이 한가할 때 동작한다. -> 다른 말로 그전까지는 할당하고 있음      
         
# HashMap vs HashTable vs ConcurrentHashMap의 차이를 설명하시오.     
**공통점 :** Map 인터페이스를 구현한 콜렉션들입니다. -> key/value 구조          
**차이점 :**    
1. HashMap : 주요 메소드에 synchronized 키워드가 없습니다. key, value에 null을 입력할 수 있습니다.     
2. HashTable : 주요 메소드에 synchronized 키워드가 선언, key, value 에 null을 입력할 수 없습니다.           
3. ConcurrentHashMap의 : HashMap을 **thread-safe** 하도록 만든 클래스가 ConcurrentHashMap입니다.     
단, key, value 에 null을 입력할 수 없으며 ```putIfAbsent```라는 메소드 가집니다.       
        
**thread-safe**    
```
멀티 스레드 프로그래밍에서 일반적으로 어떤 함수나 변수, 
혹은 객체가 여러 스레드로부터 동시에 접근이 이루어져도 프로그램의 실행에 문제가 없음을 뜻한다.
```
    
# 접근제어자에 대해 설명하시오.        
**접근 제어자가 사용될 수 있는 곳 :** 클래스, 멤버변수, 메서드, 생성자             
      
**private :**         
같은 클래스 내에서만 접근이 가능합니다.           
                  
**protected :**    
같은 패키지내에서 그리고 해당 클래스를 상속받은 자손클래스에서 접근이 가능          
       
**default :**         
같은 패키지 내에서만 접근이 가능합니다.             
        
**private :**     
접근 제한이 없습니다. -> 아무곳에서나 가능        
       
# interface와 abstract의 차이를 설명하시오.
# StringBuilder와 StringBuffer의 차이에 대해 설명하시오.
String 에 대해서 먼저 설명    
    
* **String :** immutable 클래스로 객체의 값이 변하지 않는다는 특성이 있다.     
그렇기에 ```+``` 연산시에 객체의 값을 바꾸는 것이 아니라 메모리를 새롭게 할당한다는 단점이 있습니다.      
   
* **StringBuffer** : String과 달리 mutable 클래스로 객체의 값이 변할 수 있습니다.   
그렇기에 ```+``` 연산시에 기존 메모리에 append 하는 형식, 그리고 멀티스레드시에 Syncronized 동기화 작용   
   
* **StringBuiler** : StringBuffer와 같이 mutable 클래스로 객체의 값이 변할 수 있습니다.         
그렇기에 ```+``` 연산시에 기존 메모리에 append 하는 형식,      
그러나 Syncronized 동기화를 사용하지 않아 단일 스레드시에 좋습니다.          

# try-with-resources에 대해 설명하시오.
# Synchronize에 대해 설명하시오.
# Synchronize를 하기 위한 방법은 무엇이 있나요?
# static은 메모리 구조 중 어디에 올라가나요?
# 컬렉션 프레임워크에 대해 설명하시오.
# 제네릭에 대해 설명해주시고, 왜 쓰는지 어디세 써 봤는지 알려주세요.
# Vector와 List 차이에 대해 설명하시오.
# 오버로딩과 오버라이딩의 차이는?
# CheckedException과 UnCheckedException의 차이를 설명하시오.
# OOP란 무엇인가요?
# final / finally / finalize 의 차이를 설명하시오.
# new String()과 ""의 차이에 대해 설명해주세요.
# 스프링 IOC가 무엇인가요?
# OOP와 AOP에 대한 차이를 설명해주세요.
# POJO가 무엇인가요?
