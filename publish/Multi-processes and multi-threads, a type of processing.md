두가지 모두 일을 처리하는 방식을 나타낸다는 점에서 공통점을 찾았다. 

멀티 프로세싱의 조건 : 각각의 코어가 프로세스를 실행한다. [[time-sharing]]

차이점: 멀티 스레드 같은 경우 여러개의 스레드가 하나의 공유자원을 가지고 있기에 한개의 스레드에 문제가 발생하면 다른 스레드에도 영향을 끼칠 수 있다. 하지만 멀티 프로세스는 각각 다른 메모리에 할당을 하여 철저히 독립적으로 기능할 수 있다. 하지만 메모리를 효율적으로 사용하지 못하다는 단점 또한 가지고 있다. 

### 관련한 메모 
 [[time-sharing]],[[single_core]]