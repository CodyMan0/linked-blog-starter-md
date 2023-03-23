# Iteration Interface!!
**두 가지**로 구성된다.

## 1. iterable 프로토콜 
-> iterable 객체는 **iterator 객체를 반환하는 함수**를 값으로 갖는 @@iterator 프로퍼티를 포함해야한다. (@@iterator은 Symbol.iterator에서 확인 가능 )

![[스크린샷 2022-12-03 오전 10.59.45.png|400]]
iterable 특징이 자바스크립트에 문법에 나타난 것  
1. for ... of 문
2. spread 연산
3. 구조 분해 할당 


## 2. iterator 프로토콜
Iterator 객체는 **iteratorResult**를 반환하는 next 메서드를 포함한다는 특징!!  

->  **iterator Result**
Boolean 타입의 값을 갖는 done 과 모든 타입의 값을 가질 수 있는 value 프로퍼티를 갖는다. 
![[스크린샷 2022-12-03 오전 11.06.01.png]]

(done : 순회 완료 여부 , value는 최근 순회 요소 )




관련있는 메모 : [[Spread operator syntax]] , [[구조 분해 할당]]