# selcect : I/O 완료 대기  
대부분의 운영 체제에서 사용 가능한 select()와 poll()함수, 리눅스에서 사용 가능한 epoll() 등등에 대한 액세스 제공.  
윈도우에서는 소켓에서만 작동함.  
selector 모듈은 select 모듈 프리미티브에 기반한 고수준의 효율적인 I/O 멀티플렉싱을 제공함.  
* I/O 멀티플렉싱 : 한 개의 프로세스로 두 개 이상의 클라이언트 요청을 처리하는 것.  

select.poll()  
(모든 운영 체제에서 지원되는 것은 아닙니다.)  
file descriptor 등록과 등록 해지를 지원하고 그런 다음 I/O 이벤트에 대해 폴링하는 폴링 객체를 반환합니다.  


![python_poll_sequence](https://user-images.githubusercontent.com/15919242/219988297-e2e49056-74ca-48cd-8f72-b84eb1d1ae0c.png)  
(image source : https://pythontic.com/modules/select/poll)  

