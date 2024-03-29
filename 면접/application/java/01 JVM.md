# 📕 JVM 
        
* JAVA와 OS 사이의 **중개자 역할**을 수행하여 JAVA가 OS에 종속되지 않고 재사용할 수 있도록 해준다.      
  방법으로는 바이트 코드를 OS에 맞는 기계어로 변환해주는 작업을 진행해준다.                  
* Write once, run anywhere 의 특징을 가지고 있다.         
* 스택 기반의 가상 머신으로 LIFO 원칙으로 동작한다.                   
                                  
# 📗 JVM 동작 과정과 구성 요소            
        
1. JVM은 OS로부터 프로그램이 필요로 하는 메모리를 할당받는다.            
2. JVM은 메모리를 용도에 따라 여러 영역으로 나누어 관리한다.          
3. 자바 컴파일러가 자바 소스코드를 읽어들여 자바 바이트코드로 변환시킨다.           
4. Class Loader를 통해 class 파일들을 JVM으로 로딩한다.       
5. 로딩된 class 파일들은 Execution engine을 통해 해석된다.           
6. 해석된 바이트코드는 Runtime Data Areas에 배치되어 수행이 이루어진다.            
7. 실행 과정 속에서 JVM은 필요에 따라 Thread Synchronization과 GC같은 관리작업을 수행한다.              
                
**JVM 구성 요소**   
* ClassLoader : 클래스 파일들을 JVM으로 로드 및 링크하여 RuntimeDataArea에 배치      
* ExecutionEngine : 로딩된 클래스 파일들의 바이트코드를 해석하여 JVM에서 실행가능하도록 한다.     
* **RuntimeDataArea : JVM이라는 프로세스가 프로그램을 수행하기 위하여 OS로부터 받은 메모리 공간**      
* Interpreter : 자바 바이트코드를 명령어 단위로 읽고 해석하는 역할       
* **JIT Compiler : 자바 바이트코드를 기계어로 변환시키는 역할**           
* Garbage Collect : 더 이상 사용되지 않는 메모리를 해제해주는 역할     
            
## 📖 Class Loader(클래스 로더)         
* JVM내로 `(.class)`인, 바이트코드를 로드하고, 링크를 통해 배치 작업을 수행하는 모듈.            
* Runtime 시에 동적으로 클래스를 로드한다. (지연 로딩)               
* jar파일 내 저장된 클래스들을 JVM내의 RuntimeDataArea에 배치한다.         
               
## 📖 Execution Engine (실행 엔진)      
* 로드된 클래스 파일의 바이트코드를 실행하는 런타임 모듈         
* 바이트코드를 실제로 JVM내에서 실행할 수 있는 형태로 변경한다.          

      
### 📄 Garbage collector      
메모리가 부족할 때 사용되지 않는 메모리를 해제해주며 메모리가 부족하거나 JVM이 한가할 때 동작한다.       
즉, GC의 동작 시간은 일정하게 정해져 있지 않기 때문에 언제 객체를 정리하는지는 알 수 없다.         
    
참고로, GC를 수행하는 동안 GC Thread를 제외한 다른 모든 Thread는 일시 정지상태가 된다.         
특히, Full GC가 일어나는 수 초간 모든 Thread가 정지한다면 심각한 장애로 이어질 수 있다.           
   
### 📄 Interpreter            
* 바이트코드를 명령어 단위로 읽어서 실행한다.      
* 하지만, 한 번에 한 줄씩 수행하기 때문에 느리다는 단점이 있다.       
    
### 📄 JIT Compiler (Just - in - time)   
  
런타임시에 필요에 따라 바이트코드를 기계코드로 번역해 주는 컴파일러로 Dynamic Translation이라고도 부른다.               
               
프로그램의 실행 속도를 향상시키기 위해 개발되었으며        
프로그램 실행 전에 바이트코드가 JIT Compiler에 의해 기계 코드로 번역된다.   
     
번역으로 인해 프로그램 실행 전에 지연시간이 발생하게 되지만   
대부분 인터프리터보다 훨씬 좋은 성능을 보여준다.        
 
**JIT 컴파일러 동작 기준과 원리**           
JIT Compiler가 컴파일하는 과정은 바이트코드를 인터프리팅하는 것보다 훨씬 오래걸린다.                 
그렇기 때문에 **한 번만 실행되는 코드라면 JIT Compiler 대신, 인터프리팅으로 처리를 한다**     
   
반대로, 반복, 중복으로 발생하는 바이트 코드가 있다면 JVM에서 얼마나 자주 수행되는지 체크하고(핫 스팟 디텍션)            
일정 기준을 넘는다면 `JIT Compiler`가 `ByteCode`를 기계어로 변환하고 **Caching 해놓는다.**            
   
이후, 같은 코드가 나온다면 **Caching을 사용하여 다시 번역할 필요 없이 해당 기계어를 가져와 사용한다.**           
참고로, `Caching`의 위치는 `JVM`안의 `CodeCache`에 들어간다.             
         
### 📄 JIT Compiler 기술들    
#### 🔖 Hot Spot Detection     
JIT 컴파일러를 동작시키는 기술로, ByteCode를 해석하다가 중복이 발생한다고 판단되면 기계어로 컴파일하는 방식이다.          
   
#### 🔖 Method inlining
`Method inlining`은 JIT 컴파일러에서 수행하는 최적화 방법으로            
자주 실행되는 메서드의 호출을 본문으로 대체하여 **런타임시에 컴파일된 소스 코드를 최적화**하는 방법이다.               
       
```java
public void testAddPlusOne() {
  int v1 = addPlusOne(2, 5);
  int v2 = addPlusOne(7, 13);

}
public int addPlusOne(int a, int b) {
  return a + b + 1;
}
```
```java
public void testAddPlusOne() {
  int v1 = 2 + 5 + 1;
  int v2 = 7 + 13 + 1
}
```
JIT 컴파일러는 `Method inlining`를 통해 메서드 호출의 [오버헤드](https://ko.wikipedia.org/wiki/%EC%98%A4%EB%B2%84%ED%97%A4%EB%93%9C)를 피할 수 있다.       
         
## 📖 Runtime Data Area          
* 프로그램을 수행하기 위해 OS에서 할당받은 메모리 공간     

### 📄 PC Register       
Thread가 시작될 때 생성되는 공간으로 Thread마다 하나씩 존재한다.         
Thread가 어떤 부분을 어떤 명령어로 실행해야할지에 대해 기록을 한다.     
    
### 📄 JVM 스택영역         
프로그램 실행 과정에서 임시로 할당되었다가 메서드를 빠져나가면 바로 소멸되는 데이터를 저장하기 위한 영역이다.            
메서드 호출 시 각각의 스택 프레임이 생성되며 이 안에 각종 형태의 변수나 임시 데이터, 스레드나 메서드 정보를 저장한다.         
메서드 수행이 끝나면 프레임별로 삭제를 진행한다.               

### 📄 Native method stack           
JAVA가 아닌 다른 언어로 작성된 코드를 위한 공간으로 바이트코드가 아닌 기계어로 작성된 프로그램을 실행시키는 영역이다.       
         
### 📄 Class Area              
클래스를 처음 올릴 때 초기화되는 대상을 저장하기 위한 메모리 공간이다.        
Runtime Constant Pool이라는 상수 자료형을 저장 및 참조하여 중복을 막는 별도의 관리 영역도 함께 존재한다.      
GC의 관리 대상에 포함된다.               
         
### 📄 Heap 영역                   
**인스턴스를 저장하는 가상 메모리 공간이다.**                           
인스턴스는 **소멸 방법과 시점이 다르기에 `Heap`이라는 별도의 공간이 마련**                   
Heap에 저장된 인스턴스가 참조되지 않거나 더 이상 사용되지 않을 때 `GC`가 소멸시킨다.              
