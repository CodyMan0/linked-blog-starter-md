1. Create : 새로운 프로새스
2. Destroy : 중지
3. Wait : 실행을 중지하기 위해 기다리는 함수 
4. Miscellaneous Control : 특정 프로세스 중단, 재기하는 API 
5. Status : 프로세스 정보 얻는 함수 

# Process Creation 
- parent process creates child processes.
- which, in turn creates other processes.
- finally, it forms a tree of processes

## 생성할때 나타나는 특징 
- 프로세스가 생성될땐 **자원**을 가지고 있어야한다. 
	- os와 부모가 자원을 공유할 수 있다. 
- 부모와 자식간에 **공유하는 자원** 
	-  모든 자원을 공유하거나 일부분만 공유할 수 있다.
	- 아예 공유하지 않을 수도 있다.
- **실행** 
	- 부모와 자식이 동시에 실행될 수 있고 부모가 자식 프로세스가 끝날때까지 기다리는 방식으로 동작 
	background? 뭔가 왜 필요한지를 모르겠다. 이 부분의 예시가 있을까? 
	
- child 프로세스는 address space 동일하게 복사할 수 있고 새로운 프로그램을 메모리에 로딩할 수 있다.
	UNIX example
	- 복사는 folk -> 부모와 동일한 PCB 복사, 동일한 참조값 
	- exece -> 실행하는 함수 

	- 디스크에서 바이너리 프로그램 로딩하고 초기화
관련있는 메모 : [[shallow and deep copy]]

### 프로세스 생성 요약
1. OS kernel 안에 PCB를 만든다.
2. 메모리 space 할당
3. binary program 로딩
4. 프로그램을 초기화






# Process Termination

- 운영체제의 exit 콜 혹은 다 읽히면 종료된다.

- wait API를 통해 부모가 자식 프로세스를 기다릴 수 있다. 

- 부모가 종료시킬 수있다. 
	- 자식에게 너무 많은 리소스가 들어갔을떄 






# process creation and termination

![[스크린샷 2022-12-19 오전 8.55.33.png]]
![[스크린샷 2022-12-19 오전 9.00.38.png]]

![[스크린샷 2022-12-19 오전 9.00.43.png]] 
#질문 컴파일하는 과정을 직접 보고 싶어요 승주쌤 

## wait 함수를 통해 프로세스 실행 순서를 보장 

![[스크린샷 2022-12-19 오전 9.03.23.png]]
wait 함수 : 부모가 자식의 실행 종료를 기다렸다가 다시 실행되도록 하는 것.
# exec() system call
->  여기는 코드 설명인데 와닿지 않아서 10분 정도는 제대로 집중을 못했다. 
