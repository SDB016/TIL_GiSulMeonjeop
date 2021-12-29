# 로깅  
         
## 주의점
        
**Avoid side effects**                      
* logging으로 인해 애플리케이션 기능의 동작에 영향을 미치지 않아야 한다.           
* logging 도중 NPE 발생으로 프로그램이 정상적으로 동작하지 않는 상황이 발생하면 안된다.        
        
**Be concise and descriptive**      
* 각 Logging에는 데이터와 설명이 모두 포함되어야 한다.(명확한 설명이 가능해야한다.)        
            
**Log method arguments and return values**          
* 메소드의 input과 output을 로그로 남기면 debugger를 사용해 디버깅하지 않아도 된다.          
  특히 debugger를 사용할 수 없는 상황에서는 상당히 유용하게 사용할 수 있다.          
* 메소드 앞 부분과 뒷 부분에 지저분한 중복 코드가 계속해서 발생하는 상황이 발생하는데 이는 AOP를 통해 해결할 수 있다.      
  
**Delete personal information**          
* 로그에 사용자의 전화번호, 계좌번호, 패스워드, 주소, 전화번호와 같은 개인정보를 남기지 않습니다      

# Cloud Watch   

애플리케이션 로그를 수집해서 이를 화면에 그래프로 표시해준다.   

```console
[/var/log/syslog]
datetime_format = %b %d %H:%M:%S
file = /var/log/syslog
buffer_duration = 5000
log_stream_name = {instance_id}
initial_position = start_of_file
log_group_name = [로그그룹 이름]

[/var/log/nginx/access.log]
datetime_format = %d/%b/%Y:%H:%M:%S %z
file = /var/log/nginx/access.log
buffer_duration = 5000
log_stream_name = access.log
initial_position = end_of_file
log_group_name = [로그그룹 이름]

[/var/log/nginx/error.log]
datetime_format = %Y/%m/%d %H:%M:%S
file = /var/log/nginx/error.log
buffer_duration = 5000
log_stream_name = error.log
initial_position = end_of_file
log_group_name = [로그그룹 이름]
```
       
* 시스템 로그 : CPU 사용률과 같은 인스턴스 시스템에 대한 로그를 수집한다.              
* NGINX 접근 로그 : NGINX를 통해 접근에 대한 로그를 수집한다.              
* NGINX 실패 로그 : NGINX를 통해 실패에 대한 로그를 수집한다.             

# 무엇을 모니터링해야할까?     
   
* CPU 사용률 -> 필수     
* 접근/실패 -> 애플리케이션에서도 되지만 굳이..? -> NGINX 로그를 수집하도록(IP나 접속시간 이런것들)      
* 의심점? -> 처리시간이 오래 걸릴 곳 같은곳 -> 시간 측정하고 캐시나 이런걸로 개선가능하지 않을까?      



