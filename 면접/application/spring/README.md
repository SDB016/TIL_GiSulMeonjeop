# 스프링
## 스프링이란?
  
* 자바/코틀린 웹 애플리케이션 개발을 편하게 해주는 오픈소스 프레임워크        

## 라이브러리 VS 프레임워크  
     
* 라이브러리는 단순히 도구의 모음이기에 개발자가 자유롭게 조합해서 사용이 가능        
* 프레임워크는 개발자가 도구를 사용하기 위해 다양한 조건들을 맞추면서 개발한다고 생각       

## 스프링 VS 서블렛 

클라이언트의 요청을 처리하고, 그 결과를 반환하는 Servlet 클래스의 구현 규칙을 지킨 자바 웹 프로그래밍 기술      
스프링 MVC는 서블릿을 기반으로 Dispathcer Servlet을 만들어 편리한 웹 애플리케이션 개발 환경을 제공한다.          

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


## Bean 등록과정   
## 생성자 주입을 사용해야하는 이유    

## IOC  
  
제어의 역전, 객체를 생성하고 관리하는 스프링 프레임워크에 위임하는 것을 말한다.       
스프링은 Spring Container(IoC Container)를 이용해서 빈을 관리한다.     
     
* BeanFactory     
    * 단순 빈을 저장하고 조회 하는 용도    
* ApplicationContext  
    * BeanFactory 를 상속받고 있다.    
    * 빈을 저장하는 용도외에도 국제화, 환경변수, 이벤트 처리와 같은 다양한 기능을 제공한다.   
    * 대부분의 스프링 프로젝트는 ApplicationContext 유형의 Spring Container를 이용한다.

## DI

의존성 주입 

## AOP

관점 지향 프로그래밍 


## PSA

## 스프링 빈 스코프 

* Singletone: 기본 스코프, 스프링 컨테이너의 시작과 종료까지 유지되는 가장 넓은 범위의 스코프이다.
* prototype: 스프링 컨테이너는 프로토타입 빈의 생성과 의존관계 주입까지만 관여하고 더는 관리하지 않는 매우 짧은 범위의 스코프이다.
* request: 웹 요청이 들어오고 나갈때 까지 유지되는 스코프이다.
* session: 웹 세션이 생성되고 종료될 때 까지 유지되는 스코프이다.
* application: 웹의 서블릿 컨텍스와 같은 범위로 유지되는 스코프이다.
  
## 프로토타입안에 싱글턴 객체면?   

## DL

# 스프링 MVC
## MVC란? 
## 스프링 MVC 구성요소들   
## 
