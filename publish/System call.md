System call allows user to tell the OS what to do 

OS는 다양한 interface를 제공해준다
전형적인 OS는 많은 system calls을 export한다. 

- Trap instruction 
-> 프로그램이 진행되는 과정에서 방해가 일어나면 trap이 일어난다. 
- Return-from-trap instruction 
- 트랩이 어떤 코드가 OS에서 동작해야하는지 어떻게 알지>?
-> 1. trap table , trap handler
- **System-call number**
시스템 콜에는 번호가 있어서 할당된 액션이 있다. 그 작업이 일어나서 아웃풋?
-> 자세한것 뒤에서 
![[스크린샷 2022-12-23 오전 9.46.02.png|600]]

![[스크린샷 2022-12-23 오전 9.51.47.png|600]]
#Q 이부분이 이해가 가지 않는다....

-> 내부적으로 어떻게 Limited Direction Execution protocol이 이루어진지 설명하시는데 좀 넘김.

시스템 콜의 종류
[[System call kinds]]




### 관련된 메모
[[posix CLI]]