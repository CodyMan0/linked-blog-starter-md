# 멀티 스레드란


핵심 : 처리하는 기법!
-> 프로세스 내 작업을 여러 개의 스레드, 멀티 스레드로 처리하는 기법을 말한다. 

장
1. 스레드끼리 서로 자원을 공유하기 떄문에 **메모리** 효율성이 높다. 
2. [[concurrency]] 확보
#Q 동시성 확보 
-> 한손 O 한손 x -> 동시에 작업하니 속도와 성능이 좋아진다. 


단
1. **안전성 문제** : 한 스레드에 문제가 생기면 다른 스레드에도 영향 (공유 자원이 있기에)

안전성 문제를 [[critical section]] 기법을 통해 대비한다?



## 대표적인 예시 
[[web_browser]]의 렌더링 프로세스



### 관련있는 메모 : 
[[Pros and cons of multi-threads]]

