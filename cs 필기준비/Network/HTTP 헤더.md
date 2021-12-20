# 개요 

```
START 라인
헤더 

본문
```

# STRAT LINE 

# HTTP Header 

## 구조
```  
field-name : field-value      
// field-name 은 대소문자 구분이 없다.(field-value는 있다.)   
```
 
* HTTP 전송에 필요한 모든 부가정보를 나타낸다.(바디 내용, 바디 크기, 압축, 인증, 요청 클라이언트, 서버 정보, 캐시 정보)         
* 표준 헤더들도 존재하는데 그 수가 상당하며 필요시 임의의 헤더를 추가할 수 있다.        


## 분류

1. General 헤더 : 
    * 메시지 전체에 적용되는 정보 (Connection: Close)   
2. Request 헤더 : 
    * 요청 정보 (User-Agent: Mozilla/5.0)  
3. Response 헤더 : 
    * 응답 정보 (Server:Apache)
4. Representation 헤더(엔티티 헤더) : 
    * 기존에는 Entity 헤더라는 명칭이었으나, 2014년 표준에 의해 이름이 변경되었다.   
    * **Representation(엔티티 바디)의 정보(Content-Type:text/html, Conent-Length:3423)**   

# HTTP BODY

![image](https://user-images.githubusercontent.com/50267433/146711357-b58d4075-dad2-451e-af0b-3d622007a2cc.png)

* 메시지 본문을 통해 표현 데이터를 전달한다.      
* 메시지 본문 == 페이로드(payload)       
* Representation은 요청이나 응답에서 전달할 실제 데이터다.(2014년 표준 이전에는 Entity로 명칭)        
* Representation Header는 Representation 데이터를 해설할 수 있는 정보를 제공한다.    
* 참고 : 표현 헤더는 표현 메타 데이터와, 페이로드 메시지를 구분해야 하지만, 복잡해서 이를 생략한다.   
  
# 표현(Representation)  
> 요청/응답시 바디 데이터에 대한 메타 정보    
    
* Content-Type : 표현 데이터의 형식      
* Content-Encoding : 표현 데이터의 압축 방식       
* Content-Language : 표현 데이터의 자연 언어      
* Content-Length : 표현 데이터의 길이(파싱 종료 기준)     
     
참고로 표현 헤더는 요청,응답 둘다 사용가능하다.      

# 협상(컨텐츠 네고시에이션)   
> 클라이언트가 선호하는 표현 요청   
  
* Accept : 클라이언트가 선호하는 미디어 타입 전달 
* Accept-Charset : 클라이언트가 선호하는 문자 인코딩 
* Accept-Encoding : 클라이언트가 선호하는 압축 인코딩  
* Accept-Language : 클라이언트가 선호하는 자연 언어  

참고로, 협상 헤더는 요청시에만 사용가능하다.  

**협상이라는 이름에 걸맞게 요청하는 데이터가 없다면 우선순위에 따라 데이터를 응답해준다.**   
1. 우선 순위를 지정하는 방법 
    * `Accept-Langauge:ko-KR,ko;q=0.9,en-US:q=0.8` 
    * 0~1(소수점), 클수록 높은 우선 순위이다. 생략하면 1   
2. 구체적인 것을 우선시 하는 방법
    * `Accept: text/*, text/plain, text/plain;format=flowed, */*`
    * text/plain;format=flowed -> text/plain -> text/* -> */* 순이다.     
3 요청하는 값이 아에 없으면 서버는 기본값을 보낸다.    
  
# 전송 방식 

* 단순 전송 : Content-Length  
* 압축 전송 : Content-Encoding
* 분할 전송 : Transfer-Encoding: chunked(분할해서 데이터 전송), Content-Length 안됨(분할범위 예상 안되서) 
* 범위 전송 : Content-Range: bytes 1001-2000 / 2000

# 일반 정보 

* From: 유저 에이전트의 이메일 정보   
* Referer : 이전 웹 페이지 주소 (자주 사용, `referer: 이전 url`)     
* User-Agent : 유저 에이전트 애플리케이션 정보(클라이언트 웹 브라우저 정보, 특정 브라우저 버그 파악, 통계등)         
* Server : 요청을 처리하는 오리진 서버의 소프트웨어 정보     
* Date : 메시지가 발생한 날짜와 시간     

# 특별한 정보   
  
* Host : 요청한 호스트 정보(도메인), **요청에서 필수값(동일 IP의 여러 도메인 존재하므로 명확한 도메인이름 선정)**      
* Location : 페이지 리다이렉션   
* Allow : 허용 가능한 HTTP 메서드    
* Retry-After : 유저 에이전트가 다음 요청을 하기까지 기다려야 하는 시간    
