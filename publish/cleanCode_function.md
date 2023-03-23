1. 함수, 매서드, 생성자 
 - 함수는 1급 객체
 - 그말인 즉슨 변수나 데이터에 담길 수 있다는 것 
 - 매개 변수로 전달이 가능하다는 것 (콜백함수 )
 - 함수가 함수를 반환할 수 있다는 것 (이게 고차함수) 

함수의 this 는 전역 객체 
객체의 this는 속한 객체를 바라봄
생성자 함수의 this는 생성될 인스턴스를 가르킨다 

함수는 많이 사용  -> 일반적으로 사용 


**객체는 왜 사용**? 언제 사용?->  객체


**생선자 함수**(class)는 왜 사용? 언제 사용? -> 


2. Argument(actual parameter)and Parameter(Formal parameter) 차이 
-> 파라미터는 이름이 있고 함수의 정의부분에 있따
-> argument는 함수에 들어가는 Real value

함수를 사용하는 측면에서의 벨류는 argument!! 
함수를 정의하는 측면에서의 인자는 이름이 있고 형식이 있는 것은 파라미터 


3. 복잡한 인자 관리하기 
- #투두리팩토링 객체를 사용하기
```js
function createCar (name,{brand, color, type})  {
//name은 중요하구나를 명시적으로 보여줄 수 있다. 
	return {
	name,
	brand,
	color,
	type,
	}
}
```
순서를 지킬 필요도 없다. 
그럼에도 불구하고 더 좋은 리팩토링 방법이 있다. 


인자를 안전하게 관리할 수 있도록 에러를 잘 던져주자

```Js
function createCar({name,brand,color,type}) {
  if(!brand) {
    throw new Error('brand is a required');
  }
  if(!name) {
    throw new Error('name is a required');
  }
  

}

createCar({
  name:'car',
  color: 'white',
  type:'소형'
})
```

4. 인자를 안전하게 관리할 수 있는 또다른 방법은 defaultValue를 넣어주는 것이다. 
```js
function createCar({name='티볼리',brand = 'KIA',color='white',type="중형"} = {} ) {
  
  return {
    name, 
    brand,
    color,
    type,
  }
}

createCar()
```

5. rest Parameters
- 가변인자를 취급할때 arguments 객체를 활용할 수 있었다.
```js
function sumTotal() {
  return Array.from(arguments).reduce(
    (acc,curr) => acc + curr,
  )
}

sumTotal(1,2,3,4,5,6,7,7,110)
```

하지만 인자를 받고 싶을때 문제가 생겼다. 그래서 

```js
function sumTotal(initValue, ...args) {
	//initValue : 1000
  return args.reduce(
    (acc,curr) => acc + curr,
  )
}

sumTotal(1000,1,2,3,4,5,6,7,7,110)
```
** rest Parameter로 들어온 인자는 배열로 받아진다!!?? 

6. void and return
void는 함수의 반환값이 없는 것
return 은 반환 값이 있다는 것.

기본적으로 리액트의 setState는 window alert은 void!! 그래서 return을 사용할 필요가 없다.

#좋은습관 : 내가 사용하는 API들이 리턴이 있는지 없는지 확인 (기본기!!!!)
setState는 반환값이 없다.  [[Return_Check_Moc]]

함수를 사용할떄 반환값이 있는지 없는지 생각하면서 작성하기!!! 


7. 화살표 함수
자바스크립트 화살표함수는 
1. lexical 스코프를 가지게 된다는 특징!!! 상위 실행 컨텍스트를 바라본다. this 조작법을 잘 알아야한다.
2. arguments 객체와 call , apply , bind를 사용할 수 없다는 특징
3. 내부에서 많은 것들을 사용할 수 없다. 
4. arguments 사용하고 싶을때는 rest parameter를 사용하면 더 편리하게 사용할 수 있다.
5. 화살표함수로 만든 함수는 생성자 함수로 사용할 수 없다는 특징 

```js
const Person = () => {
  this.name = name;
  this.city = city;
}

const person = new Person('poco', 'korea')

//TypeError: Person is not a constructor
```

6. 클래스와 사용할때 조심해야할 것 
```js
class Parent {
  parentMethod(){
    console.log('parentMethod');
  }
  
  parentMethodArrow = () => {
    console.log('parentMethodArrow')
  }
  
  overrideMethod = () => {
    return 'Parent'
  }
} 

class Child extends Parent {
  childMethod(){
    super.parentMethod(); // 'parentMethod'
    super.parentMethodArrow(); // TypeError: (intermediate value).parentMethodArrow is not a function
  }
  
  overrideMethod(){
    return 'Child' 
  }
}

new Child().childMethod(); // 1. this 의 특징 
new Child().overrideMethod(); // 2. 부모의 값이 호출 
```

특징 
1. 화살표 함수는 생성자 함수 내부에서 바로 초기화가 되는 특징이 있다.? 아직 정확히 모르는 듯
2. 부모 클래스 override 매소드의 화살표 함수를 바꿔주면 원하는 자식 클래스에 있는 매소드의 값이 나온다!! 왜? 


9. 콜백함수
비동기를 제어하는 기법이다? 
**함수의 실행권을 다른 함수에 위임하는 것**


```js
function register() {
  const isConfirm = confirm(
  '회원가입에 성공했습니다.')
  
  if(isConfirm) {
    redurectUserInfoPage();
  }
}

function login() {
  const isConfirm = confirm(
  '로그인에 성공했습니다.')
  
  if(isConfirm) {
    redurectIndexPage();
  }
}

// 리팩토링 

function confirmModal(message, cbFunc) {
    const isConfirm = confirm(message)
    
    if(isConfirm && cbFunc){
      cbFunc()
    }
}


function register() {
  confirmModal('회원가입에 성공했습니다.',redirectUserInfoPage)

}

function login() {
 confirmModal('로그인에 성공했습니다.',redirectIndexPage)
}


```

콜백함수는 다른 함수에게 실행권을 위임할 수 있다. 그렇게 되면 함수의 역할을 분리할 수 있게 된다,


10. 순수함수
[[redux]] ^28dddb

순수함수는 side-effect를 일으키지 않는다. 이러한 행위는 비순수함수로 바꾸는 행위
![[스크린샷 2022-12-14 오후 7.20.13.png]]

비순수 함수

```js
let numOne = 10;
let numTwo = 20;

function impureSumOne() {
return num1 + num2
}

//인자를 받고 있지 않아 언제든 변질될 수 있는 비순수함수

function impureSumTwo(newNum) {
return num1 + newNum
}

//인자는 받지만 마찬가지로 num1의 값이 예상치 못하게 변할때 출력값이 달라지는 비순수함수


function pureSum (num1, num2) {
	return num1 + num2 
}

//인풋이 동일하면 아웃풋도 동일한 순수함수 

impureSumTwo(30) // 40
num1 = 100;
impureSumTwo(30) // 130
```

자바스크립트 객체, 배열을 다루는 함수를 만드는 경우에는 새롭게 만들어서 리턴해주는 것이 좋다 !! 주의할 것 

예시
```js
const obj = {one: 1};  // obj.one의 값은 1

function changeObj(targetObj) {
  targetObj.one = 100;
  
  return targetObj
}

changeObj(obj); // obj.one의 값을 바꾸는 함수를 통과하고 난 이후 
//obj.one의 값은 1 여기는 당연하다

obj; //하지만! 원본 객체에 값이 변해버리는 심각한 상황 

-> 리팩토링

//

const obj = {one: 1};

function changeObj(targetObj) {

  return {...targetObj, one : 100}
}

changeObj(obj); // 100

obj.one // 1






```

#좋은습관 자바스크립트에서 객체를 사용할땐 함수의 리턴을 통해 새로운 객체로 만들어 반환해주는 것이 좋다.


#좋은습관 순수함수를 만든다라는 의식적인 노력이 필요하다 

[[Spread operator syntax]]
[[shallow and deep copy]]


11. closure
```js
function add(num1) {
  return function (num2){
    return function (calculateFn) {
      return calculateFn(num1,num2)
    };
  };
}


function sum(num1,num2) {
  return num1 + num2;  
}

function multiple(num1,num2) {
  return num1 * num2;  
}

const addOne = add(5)(2);
const sumAdd = addOne(sum);
const sumMultiple = addOne(multiple);


sumAdd
sumMultiple
```

실행컨텍스트로 정리해보기 

강사님이 사용한 클로저 예시  

![[스크린샷 2022-12-14 오후 7.59.27.png]]

클로저를 가장 많이 사용하는 기법
-> [[debounce and throttle]]
-> 메모리와도 관련? 