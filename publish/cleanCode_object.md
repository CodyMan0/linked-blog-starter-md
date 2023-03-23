1. shortHand property, Concise method로 코드가 보기 편해짐.

-> margin-top,right,bottom,left -> margin로 사용 (css)

```js
const fistName = 'juyoung';
const lastName = 'lee';


const person = {
	firstName: 'poco',
	lastName:'jang',
	getFullName: function () {
	return this.firstName + ''+this.lastName}
}

//shorthand 사용

const person = {
	firstName,
	lastName,
	getFullName () {
	return this.firstName + ''+this.lastName}
}
```
(js)

2. LookUp table 
-> key : value로 나열되어있는 테이블 

```js
function getUserType(type) {

switch (type) {

case "ADMIN":

return "관리자";

case "INSTRUCTOR":

return "강사";

case "STUDENT":

return "수강생";

default:

return "해당없음";

}

}

  

function getUserType(type) {

const USER_TYPE = {

ADMIN: "관리자",

INSTRUCTOR: "강사",

STUDENT: "수강생",

UNDEFINED : '해당없음 '

};

return USER_TYPE[type] || "USER_TYPE[UNDEFINED]";

}

//지역번수로 할필요도 없이 팩토리 함수 처럼 return에 바로 삽입 
function getUserType(type) {

	return (
	{

		ADMIN: "관리자",

		INSTRUCTOR: "강사",

		STUDENT: "수강생",

	}[type] ?? '해당 없음'
	);
}

  

console.log(getUserType("INSTRUCTOR"));
```

똑같은 결과인데 코드가 너무 깔끔하다 
베스트 케이스는 2번!! 모든 것들을 상수화한 코드가 베스트 왜냐하면 상수를 다른 파일에서 import해오면 더욱 보기 좋은코드 함수는 변경되지 않고 USER_TYPE만 잘 관리하면 된다. 
-> lookup table은 자바사크립트의 [] computed property와 관련있는 예!! 상수를 잘 활용해주는 것이 좋다.

3. [[구조 분해 할당]]
객체 구조 분해 할당을 하면 순서에 상관이 없어지고 넣고 싶지 않은 값은 넣지 않아도 된다. 
#설문조사리팩토링 
(인자가 세개이상일떄는 객체로 전달 

```js
function Person(name, age, location) {

this.name = name;

this.age = age;

this.location = location;

}

  

const joyoung = new Person("poceo", 14, "korea");

console.log(poco);

  

function Person({ name, age, location }) {

this.name = name;

this.age = age ?? 26;

this.location = location;

}

  

const juyoung = new Person({

location: "korea",

name: "juyoung",

});

  

console.log(poco);
```

4. Object.freeze 
```js
const STATUS = Object.freeze({

PENDING: "PENDING",

SUCCESS: "SUCCSESS",

FAIL: "FAIL",

});

  

STATUS.PENDING = "p2";

  

console.log(STATUS); // PENDING ,SUCCESS, FAIL
```

하지만 중첩 객체에는 적용이 안되는 문제가 있다. 한 Depth에서만 적용이 된다는 것이 문제. 
-> 대중적인 유틸 라이브러리!! 사용 
-> [[Typescript_Moc]]에서 readonly 기능이 있다. 
[[lodash]]


[[shallow and deep copy]]  : 얕은 복사와 깊은 복사와 연관 


5. 프로토 타입 조작을 지양하자 
왜? 
1. 자바스크립트의 내장 객체를 건드리지 말자
2. 이미 JS는 많이 발전했기때문에 생성자함수  -> class 
	1. 직접 만들어서 모듈화하기! 
	2. 직접 만들어서 모듈화하기! => npm에 베포 
-> [[Prototype]]을 건드리는 것은 상당히 위험 


6. hasOwnProperty
	보통은 for in 문에서 많이 사용한다 
```js
const person = {

name: "juyoung",

};

  

person.hasOwnProperty("name");

  

const foo = {

hasOwnProperty: function () {

return "hasOwnProperty";

},

bar: "string",

};

  

console.log(foo.hasOwnProperty("bar"));

console.log(Object.prototype.hasOwnProperty.call(foo, "bar"));

  

//hasOwnProperty는 프로토타입에 있어 보호를 받지 못해서 call을 사용해서 this를 붙혀준다.

  

// hasOwnProperty를 사용할때 다른 것들을 호출할 수 있기에 객체에 붙어서 call 매소드를 사용해야

//객체에 hasOwnProperty를 사용할 수 있다.
```

7. 상태에 직접 접근하는 것을 지양하자 
상태에 접근할 수 있는 함수를 따로 하나 만들어주자!!

[[background Flux pattern in useRuder]]

예측 가능한 코드를 작성해서 동작이 예측한 앱을 만드는 것!! 이 클린코드의 방향성 

[[getter and setter]]


