# 상태코드 

* 1xx(Informational): 요청이 수신되어 처리중   
* 2xx(Successful): 요청 정상 처리    
* 3xx(Redirection): 요청을 완료하려면 추가 행동이 필요    
* 4xx(Client Error): 클라이언트 오류, 잘못된 문법들으로 서버가 요청을 수행할 수 없음     
* 5xx(Server Error): 서버 오류, 서버가 정상 요청을 처리하지 못한다.      
   
**클라이언트가 인식할 수 없는 상태코드를 서버가 반환하면?**       
* 클라이언트는 상위 상태코드로 해석해서 처리       
* 미래에 새로운 상태 코드가 추가되어도 클라이언트를 변경하지 않아도 된다.      
* 즉, 인식하지 못할 경우, 첫글자를 통해서 문맥을 파악하면 된다.     

## 2xx(Successful)  

* 200 OK : 로직 처리가 성공했다.      
* 201 Created : 자원에 대한 조회 가능한 URL을 같이 반환한다.     
* 202 Accepted : 요청이 접수는 되었으나, 아직 처리가 완료되지 않았다.(배치 등록)     
* 204 No Content : 요청을 성공적으로 수행했지만, 응답 페이로드 본문에 보낼 데이터가 없다.  

## 3xx(Redirection)   

웹 브라우저는 3xx 응답 결과에 Location 헤더가 있으면,   
Location 위치로 자동으로 요청한다(리다이렉트)     

* 300 Multiple Choices : 
* 301 Moved Permanently : 
* 302 Found : 
* 303 See Other :
* 304 Not Modified :
* 307 Temporary Redirect :
* 308 Permanent Redirect :


## 4xx(Client Error)
## 5xx(Server Error) 
