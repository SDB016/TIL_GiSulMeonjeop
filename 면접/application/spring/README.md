# 스프링
## 스프링이란?
  
* 자바/코틀린 웹 애플리케이션 개발을 편하게 해주는 경량 오픈소스 프레임워크        

## 라이브러리 VS 프레임워크  
     
* 라이브러리는 단순히 도구의 모음이기에 개발자가 자유롭게 조합해서 사용이 가능        
* 프레임워크는 개발자가 도구를 사용하기 위해 다양한 조건들을 맞추면서 개발한다고 생각       

## 스프링 VS 서블렛 
       
클라이언트의 요청을 처리하고 결과를 반환하는 Servlet 클래스의 구현 규칙을 지킨 자바 웹 프로그래밍 기술(인터페이스)               
스프링 MVC는 Dispathcer Servlet을 만들어 편리한 웹 애플리케이션 개발 환경을 제공한다.            

## 스프링 VS 스프링 부트  
 
* 내장 톰켓을 사용하여 별도의 서버 설정없이 웹서버를 띄울 수 있다.         
* 빈들에 대한 설정을 AutoConfiguration을 이용하여 편리하게 해준다.      
* Starter 라이브러리들을 제공해주고 버전과 같은 대부분의 dependency를 관리해준다.      
* Starter 라이브러리를 지원해줘서     
   
## Spring boot stater란?  
   
특정 목적을 달성하기 위한 의존성들의 그룹으로   
응용프로그램의 종류에 따라 쉽고 빠르게 개발을 도와줄 수 있는 도구  

## AutoConfiguration 작동원리   

* spring-starter 와 같은 라이브러리들은 각각의 목적에 맞는 클래스들이 정의되어있다.              
* spring.factories 파일에는 AutoConfiguration 내용에 의해 bean 으로 생성될 클래스들의 이름이 있다.          
* spring-starter 와 같은 라이브러리들은 사실 해당 라이브러리의 클래스들을 빈으로 등록하는 Cofiguration 클래스로 구성되어있는데    
  spring-configuration-metadata.json 이나 spring-configuration-metadata.properties로 설정된 값을 통해 빈을 등록하고 있다.    
* 즉, 우리가 properties 나 json 파일을 덮어씀으로서 손쉬운 환경설정을 지원해줬던 것이다.     

## IOC  
      
제어의 역전이라는 뜻으로,    
객체를 생성하고 관리하는 책임과 역할을 스프링 프레임워크에 위임하는 것을 말한다.       
스프링은 Spring Container(IoC Container)를 이용해서 빈을 관리한다.     
     
* BeanFactory     
    * 단순 빈을 저장하고 조회 하는 용도    
* ApplicationContext  
    * BeanFactory 를 상속받고 있다.    
    * 빈을 저장하는 용도외에도 국제화, 환경변수, 이벤트 처리와 같은 다양한 기능을 제공한다.   
    * 대부분의 스프링 프로젝트는 ApplicationContext 유형의 Spring Container를 이용한다.

## DI(의존성 주입)  
   
스프링 컨테이너에 등록된 빈이 의존 객체를 직접 생성하는 것이 아니라       
스프링 컨테이너로부터 의존 객체를 주입받아 사용하는 것을 의미한다.(의존 객체도 빈 등록되어 있어야한다.)       

**주입 방법**    
* 생성자 주입   .  
* Setter 주입    
* 필드 주입      
* 메서드 주입   

**주입 흐름**   
1. 빈을 등록한다.  
2. 빈과 관련된 의존관계를 주입해준다.   
         
단, 생성자 주입 같은 경우 빈을 등록하는 동시에 의존관계를 주입한다.            
이같은 특징으로 생성자 주입은 애플리케이션을 로딩할 때 순환 참조가 발생하는 것을 사전에 알 수 있다.        
더불어, 객체 내부 상태의 재할당을 막아주고 불변을 지키려면 생성자 주입을 사용하는 것이 좋다.        
   
## AOP
        
AOP는 관점지향 프로그래밍으로서,            
애플리케이션의 핵심 로직과 부가기능 로직을 분리하여          
객체가 비즈니스 로직에 집중하는 코드를 작성해준다.         
      
Spring AOP는 **JDK dynamic proxy**로 이루어져있다.(인터페이스 기반)            

* Joinpoint: AOP가 적용될 수 있는 메소드, 필드, 객체, 생성자 등의 요소
* Pointcut: AOP 적용 가능 요소들 중에서 '실제 적용될 요소들'을 의미한다.
* Advice: AOP 부가 기능 로직 메서드 및 적용 시점   
* Weaving: PointCut에 Advice 메서드가 삽입되는 과정을 의미한다.
    * 컴파일 타임 위빙 : a.java -> a.clss 컴파일 될 때   
    * 로딩 타임 위빙 : 클래스파일을 클래스 로더가 메모리에 로드할 때  
    * **런타임/프록시 위빙 : 타겟 클래스에 부가 기능을 추가하도록 Proxy 객체를 만들어(감싸서) 실행**   
    * 스프링 AOP는 런타임 위빙만을 지원한다.(IOC/DI를 이용한 방법)
* Aspect: 특정 한 가지 기능에 대해 흩어진 관심사를 모듈화하여 묶은 클래스
    * PointCut + Advice를 묶은 메서드를 정의 및 관리한다  
     
SpringAOP는 프록시로 이루어져있기에, final 이랑 상속관련 문법에 영향을 받는다.     
   
## PSA
  
* PSA: 인터페이스와 DI를 활용하여 스프링이 변화하는 환경에서도 일관성 있는 추상 API 계층을 제공하는 것     
* 데이터베이스에 관계없이 동일하게 적용할 수 있는 트랜잭션 처리방식등이 있다.   
   
## Container란

컨테이너(Container)는 보통 인스턴스의 생명주기를 관리하며, 생성된 인스턴스들에게 추가적인 기능을 제공하도록하는 것   

## POJO
  
번역하면 '평범한 구식 자바 객체'로 프레임워크 인터페이스나 클래스를 구현하거나 확장하지 않는 단순한 클래스.

## Bean이란

컨테이너 안에 들어있는 객체

## Bean 생명주기
     
* 객체 생성 -> 의존 설정 -> 초기화 -> 사용 -> 소멸    

## 스프링 빈 스코프   

* singleton (default)
    * 애플리케이션에서 Bean 등록 시 singleton scope로 등록
    * Spring IoC 컨테이너 당 한 개의 인스턴스만 생성
    * 컨테이너가 Bean 가져다 주입할 때 항상 같은 객체 사용
    * 메모리나 성능 최적화에 유리
* prototype
    * 컨테이너에서 Bean 가져다 쓸 때 항상 다른 인스턴스 사용
    * 모든 요청에서 새로운 객체 생성
    * gc에 의해 Bean 제거
* request
    * Bean 등록 시 하나의 HTTP request 생명주기 안에 단 하나의 Bean만 존재
    * 각각의 HTTP 요청은 고유 Bean 객체 보유
    * Spring MVC Web Application에서 사용
* session
    * 하나의 HTTP Session 생명주기 안에 단 하나의 Bean만 존재
    * Spring MVC Web Application에서 사용
* global session
    * 하나의 global HTTP Session 생명주기 안에 한 개의 Bean 지정
    * Spring MVC Web Application에서 사용
* application
    * ServletContext 생명주기 안에 한 개의 Bean 지정
    * Spring MVC Web Application에서 사용
    
## 싱글톤안에 프로토타입 객체면?  
   
프로토 타입 스코프 빈내에 싱글톤 스코프 빈이 존재한다면 당연히, 매번 생성되어도 싱글톤이 주입된다.          
       
**싱글톤 스코프 빈내에 프로토타입 스코프 빈이 존재한다면 어떻게 될까? 🤔**          
* 외부 클래스가 이미 생성된 싱글톤이므로 프로토타입으로 동작하지 않고, 마치 싱글톤처럼 동작을 하는 빈이 된다.          
* 정확히 말하면, **프로토 타입을 사용하는 각각의 싱글톤 객체들은 서로 다른 프로토타입 반이 들어가지만 이후 바뀌지는 않는다.**         
    
**실글톤 스코프 빈내에서 프로토타입이 필요할 경우?**    
* 의존성 주입방법(DI) 보다는 의존성 탐색(DL) 방법이 나을 수 있다.     
* 스프링 : ObjectFactory -> ObjectProvider 이용  
* javax : Provider

## @Configuration(proxyBeanMethods = false)    
* CGLIB 프록시를 사용하냐 안하냐 차이  

# 스프링 MVC   
## MVC란?    
모델(Model), 컨트롤러(Controller), 뷰(View)라는 영역으로 서로 역할을 나누는 패턴을 의미한다.   
   
**컨트롤러**
* HTTP 요청을 받아서 파라미터를 검증하고, 비즈니스 로직을 실행한다.     
* 뷰에 전달할 데이터를 조회해서 모델에 담아 응답한다.      
       
**모델**    
* 뷰에서 사용될 데이터를 담는 역할을 한다.         
* 모델이 있어 뷰는 단순히 데이터를 받아 화면을 렌더링 하는 일에 집중할 수 있다.       
         
**뷰:**        
* 모델에 담겨있는 데이터를 사용해서 화면을 렌더링 한다.    

## 스프링 MVC 요청 흐름 

![126873936-e90358e2-10ac-4b6e-9343-6d0c20c523fd](https://user-images.githubusercontent.com/50267433/147079808-3c6016ae-0c3c-48ec-a7e2-7f83315a123b.png)
![128369947-d28f62a3-39a5-4bad-9180-03d6e3731142](https://user-images.githubusercontent.com/50267433/147082473-fdbc0cc2-35d6-4f1b-b039-577d66ac1f76.png)
  
1. `디스패처 서블릿`에서 `핸들러 매핑`으로부터 요청을 처리할 수 있는 핸들러를 찾는다.        
2. `디스패처 서블릿`에서 `핸들러 어뎁터 목록`에서 찾은 핸들러를 처리할 수 있는 `핸들러 어뎁터`를 찾는다.     
3. 핸들러 어댑터를 이용하여 실제 핸들러(컨트롤러)를 실행한다.       
    * 각각의 핸들러 어댑터에 알맞는 ArgumentResovler 및 ReturnValue 를 사용한다.              
    * @ResponseBody같은 경우, HttpEntityMethodProcessor 가 두 역할을 다한다.          
4. 핸들러 그리고 핸들러 어댑터로부터 `반환된 값`을 `뷰 리졸버`를 통해 실제 뷰 경로로 변환한다.     
5. 뷰로 이동하면서 모델 데이터를 함께 넘겨준다.   

## 필터와 인터셉터 

![9983FB455BB4E5D30C](https://user-images.githubusercontent.com/50267433/147080168-582796d2-6aac-48aa-a446-20dad12154c3.png)

* 필터는 디스패처서블릿 앞에서 처리되며 주로 인증처리에 사용된다.   
* 인터셉터는 디스패처서블릿과 핸들러 사이에 위치하여 주로 인가처리에 사용된다.     

## Aware 인터페이스들 
### BeanNameAware

```java
public class MyBeanName implements BeanNameAware {

    @Override
    public void setBeanName(String beanName) {
        ...
    }
}
```

등록된 빈의 이름을 매개변수로 받아온다.      
  
### BeanFactoryAware  
  
```java
public class MyBeanFactory implements BeanFactoryAware {

    private BeanFactory beanFactory;

    @Override
    public void setBeanFactory(BeanFactory beanFactory) throws BeansException {
        this.beanFactory = beanFactory;
    }
}
```
BeanFactory를 매개 변수로 받아올 수 있다.            
bean은 자신의 인스턴스를 생성관리하는 BeanFactory가 어떤 인스턴스인지 확인하고 접근할 수 있다.                  
이를 이용해서 커스텀 BeanFactory를 만들 수도 있을 것 같다.     

### ApplicationContextAware  

```java
public class MyAppkicationContext implements ApplicationContextAware {   
      
    @Override
    public void setApplicationContext(ApplicationContext appCtx) throws BeansException {
        ...
    }    
}
```      
ApplicationContext를 매개 변수로 받아올 수 있다.            
bean은 자신의 인스턴스를 생성관리하는 ApplicationContext가 어떤 인스턴스인지 확인하고 접근할 수 있다.                  
이를 이용해서 커스텀 ApplicationContext를 만들 수도 있을 것 같다.           

## AOP     
### AOP란? 
      
관점지향 프로그래밍,           
핵심 기능과 부가 기능이라는 관점에서 코드를 분리..?       
     
핵심 기능과 부가 기능 로직이 함께 있을 경우, 코드의 가독성이 떨어지고 중복이 발생하고 관리하기가 어려움          
핵심 기능과 부가 기능 로직을 분리하여, 개발자는 핵심 기능에만 초점을 맞추어 개발할 수 있게끔해주고       
부가 기능의 중복을 제거하고 한번에 관리하게 해줌    
   
즉, AOP는 OOP와 대치대는 개념이 아니라, OOP를 보조하기 위한 프로그래밍 기법  

### AOP 용어
    
* Aspect : PointCut + Advice 모듈(여러개 존재 가능)   
* Advisor : 하나의 PointCut + Advice (스프링에서만 사용하는 용어)    
* JoinPoint : AOP가 적용될 수 있는 위치(클래스, 필드, 메서드 등등), 스프링 AOP는 런타임(프록시)위빙이여서 메서드만 가능     
* Pointcut : JoinPoint 중에서도 실제 AOP를 적용할 대상을 정하는 것, 위와 같은 이유로 스프링은 메서드만 가능    
* Advice : 실제 AOP 적용시 적용될 부가 기능        
* weaving : 포인트 컷에서 advice를 적용하는 법       
     * 컴파일 : AspectJ 컴파일러를 이용해서 컴파일 시점에 부가기능 추가    
     * 클래스 로드 : JVM 클래스 로드시점에 AspectJ 클래스로더 조작기를 통해서 바이트 코드 조작하여 부가기능 추가        
     * 런타임 : 런타임에 부가기능 적용된 프록시 객체를 만들어서 프록시 객체 메서드 호출하면서 동작      

### AOP 프록시     

JDK Dynamic Proxy 랑 CGLIB 있음  

