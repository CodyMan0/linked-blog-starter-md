---
aliases: []
tags : 
---
Up : [[HOME 🌎]]

출처 :
저자 :
URL : 
인용 : 

- Running
	- 
- Ready
	- CPU 할당을 대기하는 상태 
- Blocked ^814f7e
	- #질문 I/O request가 시작할땐 왜 프로세스는 Blocked 상태가 되는 거지? 
	- -> 입출력 장치가 작동을하는거지 CPU는 할일이 없다. CPU 낭비하지 않고 Blocked 로 하고 Ready -> running 

## Process State Transition 
입출력이 시작되면 Running -> Blocked
입출력이 끝나면 Blocked -> Ready 
OS의 스케줄링에 의해 Ready -> Running 


예시 
- CPU만 사용 case 
![[스크린샷 2022-12-19 오전 8.23.21.png]]

- 입출력과 CPU
![[스크린샷 2022-12-19 오전 8.24.20.png]]
#질문 이게 뭐에 쓰이는지? 

### 생각의 연결고리
분야 :

키워드 :

관련있는 메모 : [[Virtualization]]
