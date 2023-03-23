
Os가 간섭하지 않는 것을 말한다.? 
![[스크린샷 2022-12-23 오전 9.31.40.png|600]]
이게 전처리 과정이다. 

위와 같이 어떤 중단과 개입없이 흘러가고 있는 것을 DIrect Execution이라고 하고 여기서 OS는 프로그램 실행시키기 위한 준비와 회수의 역할만을 진행한다. 여기서는 OS가 라이브러리처럼 사용되고 있다. 


참고:https://programming-workspace.tistory.com/32
## Direct Execution의 문제 
1. 제한된 operation :
	-  **하드웨어를 직접 다루는 연**산 
	-  Disk에 입출력 연산
	- **CPU,메모리 자원을 과도하게 사용하는 경우** 
#Q Direct Execution이란? 



## 솔루션
### 1. 유저모드와 커널모드로 접근을 제한을 두는 것 
[[UserMode]]
[[유저모드와 커널모드]]
#핵심 Direct Execution의 문제를 해결하기 위한 솔루션이었구나? O
1. userMode : 애플이 하드웨어 자원에는 모든 접근을 할 순 없는 모드
2. Kernel mode: 모든 접근이 가능한 모드
-> 프로그램 내에서 user , kernel모드로 **각각 전환**할 수 있다. 
[[System call]]이라는 함수는 커널에게 어떤 자원에 접근할 때 위임하는 함수. 

### 2.  Switching between processes
프로세스를 어떻게 다시 CPU에 접근할 수 있는지
1. [[cooperative Approach]] : system call을 기다리는 것
2. [[non-cooperative Approach]] : OS 자체가 control을 가져가는 것

-> [[Context Switching]]






