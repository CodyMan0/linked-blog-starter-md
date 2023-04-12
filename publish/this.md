
# **👉 This**

## **🙋‍♂️ This란**

최상위에서는 window 객체 
this는 **자신이 속한 객체 또는 만들어 질 인스턴스를 가리키는 변수**이다. 이해를 위해 다음 코드를 보자

```
const square = {
  distance: 5,
  getArea() {
    return square.distance ** 2;
  },
};

console.log(square.getArea());
```

square 객체의 getArea 메소드는 distance를 이용해 넓이를 계산한다. 이때 중요한 것은 square가 가지고 있는 속성인 `distance`값이 필요하다는 점이다. 객체를 선언한 변수 square를 입력하면 distance를 사용할 수는 있지만, 항상 객체를 선언한 식별자를 이용한다면 오직 square라는 이름의 객체에서만 사용이 가능해 재사용성이 떨어지게 된다.

이러한 재사용성을 고려해 객체가 어떻게 선언되는지에 상관없이, 어떤 이름의 인스턴스인지 상관없이 **항상 자기 자신을 참조할 수 있는 변수**가 바로 this라고 이해할 수 있다.

위를 객체 리터럴, 생성자함수, class로 다음과 같이 표현할 수 있다.

```
const square1 = {
  distance: 5,
  getArea() {
    return this.distance ** 2;
  },
};

function ProtoSquare(distance) {
  this.distance = distance;
}
ProtoSquare.prototype.getArea = function () {
  return this.distance ** 2;
};

const square2 = new ProtoSquare(5);
console.log(square2.getArea());

class ClassSquare {
  constructor(distance) {
    this.distance = distance;
  }
  getArea() {
    return this.distance ** 2;
  }
}

const square3 = new ClassSquare(5);
console.log(square3.getArea());

```

이러한 this는 "어떻게" 결정되는 걸까?

## **👍 this가 결정되는 방식**

this는 함수가 ==어떻게 `호출되느냐`에 따라 동적==으로 결정되는데, this 바인딩에는 4가지 규칙이 있다. 4가지 규칙에 대해 알아보자.

### **1) 기본바인딩**

객체의 메소드나 생성자 함수를 제외한 함수들, 일반함수로 함수 내부에서 this를 호출하면 `전역객체`를 얻을 수 있다. 전역객체는 브라우저냐 Node.js냐에 따라 각각 window와 global을 의미한다. 브라우저 기준으로 전역객체는 window로 설명을 진행하려 한다.

```
function hi(){
    console.log(this) //window 또는 global
}
hi()
```

이때 메소드 내부 중첩 함수나 콜백함수가 일반함수로 호출될 경우에도 동일하게 전역 객체로 this 바인딩이 된다.

```
var value = 1;

const obj = {
  value: 100,
  foo() {
    setTimeout(function () {
      console.log(this);// window
      console.log(this.value);// 1
    }, 100);
  },
  too() {
    function bar() {
      console.log(this);// window
      console.log(this.value);// 1
    }
    bar();
  },
};

var value = 1;

const obj = {
  value: 100,
  too() {
    'use strict';
    function bar() {
      console.log(this); // undefined
      console.log(this.value); // Uncaught TypeError: Cannot read properties of undefined
    }
    bar();
  },
};

obj.too();
```

이때 use strict로 엄격모드를 적용하면 전역객체는 기본 바인딩에서 제외되어 this.value는 에러를 던지게 된다.

### **2) 암시적 바인딩**

호출할 때의 객체의 존재 여부에 따라, this는 만들어진 객체에 속해지지 않고, `호출한 객체, 컨텍스트 객체`에 바인딩된다. 이것을 **암시적 바인딩**이라 하는데 이해를 위해 다음 예제를 보자.

```
const person = {
  name: 'lee',
  getName() {
    return this.name;
  },
};

console.log(person.getName()); //lee

const anotherPerson = {
  name: 'kim',
};

anotherPerson.getName = person.getName;
console.log(anotherPerson.getName()); //kim

const getName = person.getName;
console.log(getName());// window

```

위의 코드를 보면 getName이 **함수가 사용되는 곳에 따라 this가 달라진다**. 객체에서 선언된 this라면 해당 객체와 binding이 되어야 하지만, 호출하는 객체가 누구냐에 따라 달라지는 결과를 보여준다. 그렇기 때문에 함수가 가리키는 객체는 독립적인 `컨텍스트 객체`라고 볼 수 있다.

```
function foo() {
  console.log(this.text);
}

var name = {
  text: '영준',
  foo: foo,
};

var person = {
  text: '가영',
  name: name,
};

person.name.foo();// 영준

```

만약 중첩된 상태에서 호출하게 된다면 가장 가까운 객체, name을 암시적으로 컨텍스트 객체로 바인딩한다.

이렇게 어디서 호출하냐에 따라 달라지면 예측하기 어렵고 에러가 발생할 수 있다. this binding을 우리가 정하는 방법은 없을까?

### **3) 명시적 바인딩**

this binding을 명시적으로 정해주는 방식에는 apply, call, bind 메소드를 사용하는 방법이 있다.

### **apply와 call**

두 가지 메소드는 사용 시 전달한 객체를 this에 바인딩하고, 호출한다. 두가지 메소드의 차이점은 함수에 인자를 전달하는 방식에 있다. apply는 배열로 인자를 전달하고 call은 하나 하나씩 전달하고 호출한다.

```
function getThisBinding() {
  console.log(arguments);
  return this;
}

const thisArg = { a: 1 };
console.log(getThisBinding());
console.log(getThisBinding.apply(thisArg, [1, 2, 3])); //[1, 2, 3]
console.log(getThisBinding.call(thisArg, 1, 2, 3));//[1,2,3]

```

### **bind**

bind는 this만 바인딩하고 호출은 하지 않는다. 콜백함수나 중첩함수가 일반함수로 호출되었을 때, this가 달라지는 문제를 명시적으로 해결해 줄 수 있다.

```
const person = {
  name: 'lee',
  foo(callback) {
    setTimeout(callback.bind(this), 100);
  },
};

person.foo(()=> {
  console.log(this.name); //lee
});

```

### **4) new 바인딩**

생성자함수 내부의 this는 인스턴스가 바인딩된다.

```
function foo() {
  this.name = '영준';
  this.callName = function () {
    console.log(this.name);
  };
}

const bar = {
  name: '주희',
};

const x = new foo();
x.callName.bind(bar);
x.callName();// 영준

```

생성자 함수를 이용해 만든 x 객체에 명시적 바인딩인 bind로 bar를 바인딩하려했지만, new 바인딩이 우선순위가 높아 "영준"으로 나온 것을 볼 수 있다.

### **🔼 예외적인 바인딩: 화살표 함수**

앞서 설명한 this 바인딩과는 다르게 작용한다.화살표 함수는 함수 자체가 this를 갖지 않아 함수 선언 시의 **상위 스코프의 this를 바인딩**한다. 항상 this를 보장하기 때문에 callback함수에서 주로 사용된다.


```
const foo = {
  name: '영준',
  bar: () => console.log(this.name),
};

foo.bar(); // undefined

const boo = {
  name: '영준',
  far() {
    console.log(this.name);
  },
};

boo.far(); //영준

```

하지만 주의할 점은 메소드를 화살표함수로 만들게 되면 foo 객체가 아니라 상위 스코프의 this인 전역객체를 binding하게 된다. 그렇기 때문에 메소드는 메소드 축약으로 정의하는 게 낫다는 것을 알 수 있다.

## **마치며**

this 바인딩은 예상치 못하는 에러를 만들 수 있기 때문에 꼭 한번 정리를 하고 넘어가야 했다. 아직 화살표 함수에서 마지막 부분이 왜 전역객체를 바인딩하는지 잘 이해가 되지 않아 생성자함수와 prototype에 대해서 정리하고 다시한번 확인을 해보려고 한다.


## 4.10 this 정리 
### 객체 리터럴 방식으로 생성한 객체
객체 리터럴 방식으로 생성한 객체는 메서드 내부에서 메서드 자신이 속한 객체를 가리키는 식별자를 재귀적으로 참조할 수 있다는 것. 

자신이 속한 객체를 재귀적으로 참조하는 것은 바람직하지 않다 그래서 생성자 함수와 class 방식을 알아보자 

### 생성자 함수 방식
```js
function Circle(radius){
	????.radius = radius;
}

Circle.prototype.getDiameter = function (){
return 2 * ????.radius
}

// 생성자 함수로 인스턴스를 생성하려면 먼저 생성자 함수를 정의해야 한다. 
```

생성자 함수를 정의하는 시점에는 아직 인스턴스를 생성하지 이전이다. 그래서 생성자 함수가 생성할 인스턴스를 가리키는 식별자를 알 수가 없는 문제가 있다. 따라서 **자신이 속한 객체** 또는  **자신이 생성할 인스턴스를 가르키는 특수한 식별자**가 this이다

this는 [[V8 engine]]에 의해서 암묵적으로 성생되고 코드 어디서든 참조할 수 있다. 

this 바인딩은 함수 호출 방식에 의해 동적으로 결정된다.  -> 동적 스코프!!?? 
함수는 정적 스코프를 취하는데 반대 개념 찾았다.

```js
function Circle(radius){
	this.radius = radius;
}

Circle.prototype.getDiameter = function (){
return 2 * this.radius
}

// 인스턴스 생성
const circle = new Circle(5);
console.log(circle.getDiameter()) // 10
```

자바나 C++은 this binding이 항상 클래스가 생성하는 instance를 가리키지만 자바스크립트는 함수가 호출되는 방식에 따라 this가 동적으로 결정된다. 

전역 : window 객체
일반 함수 스코프 : window 객체 
객체의 매소드 스코프 : 해당 객체를 가리킨다. 
생성자 함수 : 만들어질 인스턴스를 가리킨다. 

[[strict mode]]에서는 일반 함수 내부의 This에 window가 뜨지 않고 undefined가 바인딩된다. 

[[함수 in js]]의 스코프 결정 방식은 렉시컬 스코프(정적 스코프)이지만 자바스크립트에서 this값이 바인딩되는 방식은 동적 스코프를 취하고 있다. 즉 함수가 호출되는 방식에 따라 this 값이 할당된다는 것.

### 다양한 함수 호출 위치 
1. 일반 함수 호출
2. 메서드 호출
3. 생성자 함수 호출
4. 프로토타입을 활용한 간접 호출

```js
const foo = function () {
	console.dir(this);
};

// 1. 일반 함수 호출
foo(); // window

const obj = {
	foo,
};

// 2. 메서드 호출
 obj.foo(); // obj


// 3. 생성자 함수 호출
new foo(); //foo {}


// 4.프로토타입을 활용한 간접 호출



```

#### 일반 함수 호출 
기본적으로 this에는 전역 객체가 바인딩된다. 쉽게 정리해보면 일반함수가 콜백 함수로 호출이 되건 매소드 안에서 일반함수로 호출이 되건 모두 this는 전역을 가리킨다. 이게 문제다. 

```js
var value = 1;

const obj = {
	value: 100,
	foo() {
		console.log("fooThis", this);
		setTimeout(function () {
			console.log("callbackThis", this);
			console.log("callbackThis", this.value);
		}, 100);
	},
};

obj.foo();
```

##### 해결 1 함수 외부에서 This값을 변수에 담아 사용하는 방법

```js
var value = 1;

const obj = {
	value: 100,
	const that = this
	foo() {
		console.log("fooThis", this);
		setTimeout(function () {
			console.log("callbackThis", this.value); // 100
		}, 100);
	},
};

obj.foo();
```


##### 해결 2 bind를 활용한 명시적 바인딩
```js
var value = 1;

const obj = {
	value: 100,
	foo() {
		console.log("fooThis", this);
		setTimeout(function () {
			console.log("callbackThis", this.value); // 100
		}.bind(this), 100);
	},
};

obj.foo();
```

##### 해결 3 arrow function을 활용하여 this 바인딩
```js
var value = 1;

const obj = {
	value: 100,
	foo() {
		console.log("fooThis", this);
		setTimeout(() => console.log("callbackThis", this.value), 100);
	},
};

obj.foo();

```

#### 메서드 호출 
#### 생성자 함수 호출 
생성자 함수의 내부의 this에는 추후에 생성할 인스턴스가 바인딩된다. 

#### 프로토타입 매소드에 의한 간접 호출
.apply .call .bind는 모든 함수가 상속받아서 사용할 수 있다. 

- apply 와 call 특성
-> ==본질적으로 함수를 호출하는 기능을 수행한다.== 
-> 두개의 차이는 호출할 함수에 **인수를 전달하는 방식**만 다르다. 
-> apply는 리스트의 형태로 call은 쉼표로 나눠 인자를 전달한다.
```js
console.log(getThisBinding.apply(thisArg, [1, 2, 3]));
console.log(getThisBinding.call(thisArg, 1, 2, 3));
```

- bind 특성
-> ==함수를 호출하지 않는다는 특징이 있다.==  다만 첫번째 인수로 전달된 값으로 this 바인딩이 교체된 함수를 리턴한다. 
```js
console.log(getThisBinding.bind(thisArg)); // getThisBinding
console.log(getThisBinding.bind(thisArg)()); // {a :1}
```


```js

const person = {
	name: "lee",
	foo(callback) {
		setTimeout(callback, 100);
	},
};

person.foo(function () {
	console.log(`Hi my name is ${this.name}`); // undefined
});


const person = {
	name: "lee",
	foo(callback) {
		setTimeout(callback.bind(this), 100);
	},
};

person.foo(function () {
	console.log(`Hi my name is ${this.name}`); // lee
});

```


![[스크린샷 2023-04-10 오후 5.27.49.png]]