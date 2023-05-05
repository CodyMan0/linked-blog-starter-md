
# ** This**

## **🙋‍♂This란**

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

자바나 C++은 this binding이 항상 클래스가 생성하는 instance를 가리키지만 자바스크립트는 함수가 호출되는 방식에 따라 this가 동적으로 결정된다. 어?? 자바스크립트에서 스코프는 동적으로 할당되지 않고 정적(렉시컬)스코프를 취한다. 스코프와 this-binding이 생성되는 방식이 다르구나라는 것을 알 수 있다. 

## 만들어지는 객체에 따라 다른 this

### 객체 리터럴 방식으로 생성한 객체
객체 리터럴 방식으로 생성한 객체는 메서드 내부에서 메서드 자신이 속한 객체를 가리키는 식별자를 재귀적으로 참조할 수 있다. 하지만 딥다이브에 정리돼있길, 자신이 속한 객체를 재귀적으로 참조하는 것은 바람직하지 않다고 한다. 그래서 생성자 함수 방식으로 만들어진 객체를 살펴보면 


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

생성자 함수를 정의하는 시점에는 아직 인스턴스를 생성하지 이전이다. 그래서 생성자 함수가 생성할 인스턴스를 가리키는 식별자를 알 수가 없는 문제가 또 발생한다. 그렇다면 어떻게 해야하는거지? 재귀적으로 참조하는 것은 바람직 하지 않다고 하고 생성자 함수 방식으로 생성할 경우 정의된 함수 스코프 시점에서는 미래에 생길 인스턴스를 가르키는 식별자를 알 수 없다고 하고... 크흠

결론적으로 **자신이 속한 객체** 또는  **자신이 생성할 인스턴스를 가르키는 특수한 식별자**가 this이다

> 이러한 this는 "어떻게" 결정되는 걸까?

## **👍 this가 결정되는 방식**

this는 함수가 ==어떻게 `호출되느냐`에 따라 동적==으로 결정되는데, **this 바인딩**에는 4가지 규칙이 있다. 

4가지 규칙에 대해 알아보자.

### **1) 기본바인딩** (일반 함수 호출)

객체의 메소드나 생성자 함수를 제외한 함수들, 일반함수로 함수 내부에서 this를 호출하면 `전역객체`를 얻을 수 있다. 전역객체는 브라우저냐 Node.js냐에 따라 각각 window와 global을 의미한다. 브라우저 기준으로 전역객체는 window로 설명을 진행하려 한다.

```
function hi(){
    console.log(this) //window 또는 global
}
hi()
```

이때 메소드 내부 중첩 함수나 **콜백함수**가 일반함수로 호출될 경우에도 동일하게 전역 객체로 this 바인딩이 된다. (콜백함수도 일반함수로 호출된다는 것, 그렇기에 화살표 함수를 활용할 수 있다.)

```
var value = 1;

const obj = {
  value: 100,
  foo() {
    setTimeout(function () {
      console.log(this);// window
      console.log(this.value);// 전역의 value :1
    }, 100);
  },
  too() {
    function bar() {
      console.log(this);// window
      console.log(this.value);// 전역의 value :1
    }
    bar();
  },
};

var value = 1;

const obj = {
  value: 100,
  too() {
    'use strict'; // use strict을 작성할 경우는 window에 접근할 수 없습니다. 
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
function read() {
  console.log(this.text);
}

var memos = {
  text: '주영메모장',
  memo: memo,
};

var memo = {
  text: '메모',
  read: read,
};



memos.memo.read();// 메모

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
  this.name = '주영';
  this.callName = function () {
    console.log(this.name);
  };
}

const bar = {
  name: '재건',
};

const x = new foo();
x.callName.bind(bar);
x.callName();// 주영

```

생성자 함수를 이용해 만든 x 객체에 명시적 바인딩인 bind로 bar를 바인딩하려했지만, **new 바인딩이 우선순위가 높아** "주영"으로 나온 것을 볼 수 있다.

### **🔼 예외적인 바인딩: 화살표 함수**
[[arrow function]]
앞서 설명한 this 바인딩과는 다르게 작용한다.화살표 함수는 함수 자체가 this를 갖지 않아 함수 선언 시의 **상위 스코프의 this를 바인딩**한다. 항상 this를 보장하기 때문에 callback함수에서 주로 사용된다.


```js
// 객체 매소드로 화살표 함수 사용
const foo = {
  name: '주영',
  bar: () => console.log(this.name),
};

foo.bar(); // undefined

// 객체 매소드로 메소드 축약 사용

const boo = {
  name: '주영',
  far() {
    console.log(this.name);
  },
};

boo.far(); //주영

```

하지만 주의할 점은 메소드를 화살표함수로 만들게 되면 foo 객체가 아니라 상위 스코프의 this인 전역객체를 binding하게 된다. 그렇기 때문에 메소드는 메소드 축약으로 정의하는 게 낫다는 것을 알 수 있다.

## this 바인딩을 공부를 마치며
약 8개월간, this 바인딩을 모르고 프로젝트를 진행했음에도 불구하고 불편했던 적이 없었다. 하지만 클래스 객체를 활용하여 네트워크 에러를 관리하거나 코드 내에서 중복이 많은 API 호출등의 클래스를 다루기 시작하면서 this의 지식의 필요성을 느꼈다. 처음부터 알 필요는 없다고 생각되며, 단계에 맞게 알아가면 된다고 생각한다. 


