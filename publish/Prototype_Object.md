프로토 타입은 상위 객체 역할을 수행하고 하위 객체에 프로퍼티를 제공한다. 

- 모든 객체는 [[Prototype]]이라는 내부 슬롯을 가지고 있다. 
- 하위에서 접근하기 위해서는 `__proto__` 접근자 프로퍼티를 통해 자신의 프로토타입에 간접적으로 접근할 수 있다. 

`__proto__`가 무엇이냐 -> 객체와 객체를 **연결하는** 링크

`__proto__`에 의해 `[[ProtoType]]`에 접근하도록 만들어진 이유는 참조에 의해 상호적으로 프로토타입 체인이 생성되는 것을 방지!! 


# 코드내 `__proto__` 사용 자제
프로토 타입의 참조를 취득하고 싶으면 **Object.getPrototypeOf**
교체하고 싶을때는 **Object.setPrototypeOf**






