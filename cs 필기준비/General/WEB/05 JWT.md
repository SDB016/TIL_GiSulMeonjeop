# JWT 

JWT는 하나의 인터넷 표준 인증 방식으로 인증에 필요한 정보들을 Token에 담아 암호화시킨다.      
Cookie와 크겓 다르지는 않지만, 강조되는 점은 **서명된 토큰**이라는 것이다.     
              
공개/개인 키를 쌍으로 사용하여 서명할 경우             
개인 키를 보유한 서버가 이 서명된 토큰이 정상적인 토큰인지 인증할 수 있다는 것이다.        
이러한 JWT의 구조 때문에 인증 정보를 담아 안전하게 인증을 시도하게끔 전달할 수 있는 것이다.      
  
**구성요소**  
* Header : 토큰 타입, 서명 생성 알고리즘 
* Payload : 실제 데이터 본문 
* Signature : 

## Header   

```json
{
  "typ": "JWT",
  "alg": "HS512"
}
```  
header에는 보통 토큰의 타입이나, 서명 생성에 어떤 알고리즘이 사용되었는지 저장한다.     

## Payload  

```json
{
  "sub": "1",
  "iss": "ori",
  "exp": 1636989718,
  "iat": 1636987918
}
```
playload 은 보통 Claim 이라는 사용자/토큰에 대한 프로퍼티를 Key-Value 형태로 저장한다.   
Claim이라는 말 그대로 토큰에서 사용할 정보의 조각을 의미한다.     
  
**JWT 표준 Claim 스펙**     *
1. iss(Issure): 토큰 발급자 
2. sub(Subject): 토큰 제목(사용자에 대한 식별값)    
3. aud(Audience): 토큰 대상자  
4. exp(Expiration Time): 토큰 만료 시간  
5. iat(Issued At): 토큰 발급 시간
6. nbf(Not Before): 토큰 활성 날짜(이 날짜 이전의 토큰은 활성화 되지 않음을 보장)   
7. jti(JWT id): JWT 토큰 식별자(Issure가 여럿일 경우 사용한다)   

JWT 표준 Claim 스펙은 단순히 스펙일 뿐이지 꼭 이 7가지만 사용해야하는 법은 없다.    
상황에 따라 사용하고 필요시 사용자가 커스텀하게 만들어 사용할 수 있다.    
        
**단, 중요한 것은 payload 에는 민감한 정보를 담지 않아야한다.**           
header와 payload의 경우 base64로 인코딩 되어있을 뿐이지 특별한 암호화가 걸려있는 것이 아니다.            
누구나 jwt를 가지고 있다면 base64 디코딩을 통해 header나 payload에 담긴 값을 알 수 있다.        
그렇기 때문에 JWT Payload는 단순히 **식별하기 위한 정보**만을 담아두는게 좋다.    
      
**그렇다면, Header와 Payload에도 암호화를 해야하지 않나? 🤔**         
* 아니다. 만약 그렇게 한다면 매 요청시마다 복호화하는 작업을 추가로 진행해야한다.        
* 그렇기 때문에 유출되었을 때 그렇게 큰 상관이 없는 비민감 정보를 토큰에 담는 것이 기본 스펙이다.  

## Signature
JWT에서 가장 중요한 요소인 서명이다.       

![다운로드](https://user-images.githubusercontent.com/50267433/146970625-188ee54e-b235-4bd8-8960-61cb5e25da22.png)
  
서명은 위와 같이 header를 디코딩한 값, payload를 디코딩한 값을 합치고      
이를 `your-256-bit-secret` 즉, 서버가 가지고 있는 개인키를 가지고 암호화되어있는 상태다.    
    
따라서 signature는 서버에 있는 개인키로만 암호화를 풀 수 있고           
**다른 클라이언트는 임의로 Signature를 복호화할 수 없다.**         
  
1. JWT 토큰을 클라이언트가 서버로 요청과 동시에 전달한다.      
2. 서버가 가지고있는 개인키를 가지고 Signature를 복호화한다.     
3. base64UrlEncode(header)가 JWT의 heaer값과 일치한지 확인한다     
4. base64UrlEncode(payload)가 JWT의 payload값과 일치한지 확인한다.  
5. 모든 데이터가 일치할 경우 인증을 허용한다.        
   
여기서 중요한 점은 개인키를 통해 복호화를 하는 것뿐만 아니라     
payload에 담긴 식별자가 변조된 JWT로 요청을 하더라도     
서버가 애초에 발급했던 Signature 안의 payload와 다르기 때문에 인증이 불가능해진다.  

# JWT 장점 
# JWT 단점(한계)  
   



# 참고 
RestAPI 서버는 Stateless해야한다.  


