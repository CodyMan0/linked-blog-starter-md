1. typeof: 타입 검사는 typeof로 할 수 있지만 REFERENCE 타입은 typeof로 타입 확인이 어렵다. (typeof가 만능은 아니다.  가장 문제는 null)
2. instanceof : reference 타입을 검사하기 좋다 여기에 큰 함정이 있다. 프로토 타입의 최 상위는 객체이기에 타입 검사를 하는게 어렵다...
3. Object.prototype.toString,call()
4. undefined vs null -> 
5. 웬만해서 명시적으로 타입을 변환 시키자 
6. Number.Max_Safe_INTEGER
7. Number.isNan을 하면 더 엄격한 검사를 할 수 있다 

# 타입 정리
1. PRIMITIVE (불변)

2. REFERENCE (가변) 
	1. array 
	2. funciton 
	3. Date
	4. Object
