# HTTP 헤더 

```
START 라인
헤더 

본문
```
  
**헤더 구조**
```  
field-name : field-value      
// field-name 은 대소문자 구분이 없다.(field-value는 있다.)   
```
 
* HTTP 전송에 필요한 모든 부가정보를 나타낸다.(바디 내용, 바디 크기, 압축, 인증, 요청 클라이언트, 서버 정보, 캐시 정보)         
* 표준 헤더들도 존재하는데 그 수가 상당하며 필요시 임의의 헤더를 추가할 수 있다.        


## 헤더 분류

1. General 헤더 : 
    * 메시지 전체에 적용되는 정보 (Connection: Close)   
2. Request 헤더 : 
    * 요청 정보 (User-Agent: Mozilla/5.0)  
3. Response 헤더 : 
    * 응답 정보 (Server:Apache)
4. Representation 헤더(엔티티 헤더) : 
    * 기존에는 Entity 헤더라는 명칭이었으나, 2014년 표준에 의해 이름이 변경되었다.   
    * **Representation(엔티티 바디)의 정보(Content-Type:text/html, Conent-Length:3423)**   
   
### HTTP BODY

![image](https://user-images.githubusercontent.com/50267433/146711357-b58d4075-dad2-451e-af0b-3d622007a2cc.png)

* 메시지 본문을 통해 표현 데이터를 전달한다.      
* 메시지 본문 == 페이로드(payload)       
* Representation은 요청이나 응답에서 전달할 실제 데이터다.(2014년 표준 이전에는 Entity로 명칭)        
* Representation Header는 Representation 데이터를 해설할 수 있는 정보를 제공한다.    
* 참고 : 표현 헤더는 표현 메타 데이터와, 페이로드 메시지를 구분해야 하지만, 복잡해져서 이를 생략한다.   

