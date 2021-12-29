# 로깅  



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



