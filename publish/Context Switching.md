context라고 하면 process의 register context를 말한다. 


Context Switching은 프로세스를 바꾼다는 의미이고 더 자세히 말하면 [[PCB]]를 교환하는 과정을 말한다. 

Context switching을 하는 시간은
[[오바헤드]]라고 한다. 

Context switching할때 걸리는 시간은 하드웨에어 의존적이다. 

[[캐시미스]]가 생기는 이유 : 컨텍스트 스위칭이 일어날 때 프로세스가 가지고 있는 메모리 주소가 그대로 있으면 잘못된 주소 변환이 생기므로 캐시 클리어 과정을 겪게 되고 이 떄문에 캐시미스가 발생합니다. 음...


### 과정 
register value를 kernel stack에 저장하고 다른 프로세스의 커널 스텍에 있는 PCB와 switching 


