[출처](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object/proto)
자바스크립트는 명령형 , 함수형, 프로토타임 기반, 객체 지향 언어


Q. 공부하고 보니 [[scope chain]]과 상당히 비슷. 외부환경레코드의 개념과 동일한 것 같다. 

# 프로토 타입 이해
![[스크린샷 2022-12-17 오후 12.17.52.png]]
객체를 만들면 있는 `__proto__`가 있다. 
Q. `__proto__`는 왜 getter와 setter로 이루어진 함수로 만들어졌을까 


## 중요한 개념 
-> 어제 공부한 부분 다시 던져놓고 정리해보기 
-> 클래스는 프로토 타입을 편하게 사용할 수 있도록 syntatic sugar
-  [ ] 체크 포인트 


- 프로토 타입은 내용을 복사하지 않고 상속을 구현할 수 있게 해주는 방법 

- 프로토타입은 **연결**하는 것


# 프로토 타입의 두 영역  
## instance와 직접접인 변수
instance 내부에 존재

## static 
변하지 않는 값, 부모의 프로토타입에 위치 

-> this 바인딩 , 객체 생성 방식 


- keyword
[[Prototype_Object]]
[[Prototype_Chain]]
[[To understand the connection between objects]]
[[Prototypes based on how objects are created]]

정리 
1. 프로토타입은 자식으로 가는게 아니라 자바스크립트 내부에서 슬롯에 있고 링크로 접근할 수 있다는 것. 


### 관련있는 메모 
[[getter and setter]]