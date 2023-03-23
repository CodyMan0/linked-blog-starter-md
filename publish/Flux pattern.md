## 기본 개념 
![[mvcAndFlux.png]]



배경 : 기존의 MVC 패턴의 한계 (규모가 커지면 model과 view의 인과관계가 복잡해지는 것)로 인해 flux 아키택처가 등장하였다. 

정의 : **단방향 데이터 흐름**을 통해 보다 **예측 가능**하게 상태를 관리할 수 있는 클라이언트 사이드 웹 어플 아키텍쳐 

1. [[action]]  : 앱에서 어떤 부분이 변경되어야하는지 dispatcher에게 전달 
- ajax or view에서 발생한 상태 변경 요청 
2. [[dispatcher]] : action을 받으면읽고 어느 부분이 변경될지 정한다. (action hub)
- 동기 실행이 특징이 있다. 그래서 다수의 액션이 들어올때 순차적으로 실행하게 된다.
- 모든 action을 정리하여 전달하는 역할 
3. [[store]] : 모든 상태와 관련된 로직을 가지고 있다.
4. view  : 다시 그려지는 컴포넌트 

### 준비 과정 요약 
 1. store는 dispatcher에게 액션을 달라고 요청
 2. view는 store한테 최신 상태 묻고 최신 상태 전달 
 3. view는 하위 컴포넌트에게 전달
 4. view는 상태가 바뀌면 store에게 알려달라고 한다, 

### 데이터 흐름 요약
1. view는 action 에게 요청 
2. action을 포멧에 맞게 dispatcher에게 넘겨주고 
3. dispatcher은 알맞은 순서로 store에 보내고 값을 업데이트 한다.
4. store에서 상태 변경이 완료되면 view에게 값을 보낸다. 
5. 새로운 상태를 받으면 모든 뷰에게 알린다. 
 



## 장점과 한계 
### 장점
데이터 흐름의 구조화 및 쉬운 유닛 테스트


### 한계
높은 학습 곡선 및 장황한 문법  



### 관련있는 메모
1. [[redux]]
2. [[MVC pattern]]
3. [[pure function]]