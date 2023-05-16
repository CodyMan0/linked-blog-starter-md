
# 운영체제의 핵심
시스템의 전반을 관리하는 역할
하드웨어와 관련된 작업을 직접 수행 !


# 순서
1. 프로그램의 현재 CPU 상태를 저장한다. 
-> 나중에 다시 돌아갈 위치를 파악해놓는것
2. 커널이 interrupt와 system call을 직접 처리한다. 
3. 처리가 완료되면 중단됐던 프로그램의 cpu 상태를 복원 
4. 다시 통제권을 유저모드에게 준다.

# 만들어진 이유
시스템을 안정적으로 동작할 수 있도록, 보호하기 위해 
  
**KernelMode라는 것은 모든 System Memory와 모든 명령어들에 접근이 가능한 실행모드**를 말한다.


OS(운영체제)의 핵심 부분이라고 말할 수 있다. Kernel에서는 **CPUScheduling(CPU 스케쥴링),**

**Memory Management(메모리 관리), IO Management(입출력 관리), File System Management(파일 시스템 관리)등의 일**을 한다.