# 코드

![[스크린샷 2022-12-15 오후 2.15.06.png|400]]

#Q 출력의 순서는 OS 의 스케쥴러가 어떻게 되어있는지에 따라 다르다? 

![[스크린샷 2022-12-16 오후 3.59.54.png|400]]
Q. 컴퓨터를 사용할떄 수많은 프레세스에게 마치 CPU가 하나씩 있는 것 처럼 하는 방법이 CPU virtualization 

필요한 것 
- 도구 (메커니즘): [[Context Switching]] 
- 지능 (정책): [[scheduling Policy]]
- 

![[스크린샷 2022-12-16 오후 4.10.03.png|400]]
CPU 가상화를 위해서는 실제로 OS가 [[interleaving]]을 컨드롤 한다

프로세스 A , 프로세스 B 가 있는데 프로스세 A가 진행되다가 OS 코드에서 interleaving하여 프로세스 B가 진행되는 것. 


[[Problems with virtualizing CPUs]]


### 관련있는 메모 
[[CPU]]