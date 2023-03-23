1. **javaScript의 배열은 객체이다**
![[스크린샷 2022-12-13 오후 3.57.24.png|300]]
2. **Array.length** 
-> 항상 조심해야한다. 자바스크립트 배열에는 구멍이 있다. 
array.length는 배열의 마지막 인덱스의 요소이다. 그래서 구멍이 있다. 
 
![[스크린샷 2022-12-13 오후 4.01.22.png]]
//4 
//10
그사이는 빈다.  

또하나의 예시  
```js
Array.prototype.clear = function () {

this.length = 0;

};

  

function clearArray(array) {

array.length = 0;

  

return array;

}

  

const arr = [1, 2, 3];

  

console.log(arr.clear());

console.log(clearArray(arr));
```

배열의 length를 바꿨을뿐인데 배열이 초기화됐다. 그만큼 length는 조심해야한다. 마지막 index를 표출하는 length라는 것을 기억해야한다. 


3. **배열 요소에 접근하기** 
요소에 접근할때 arr[0], arr[1]만으로는 읽는이가 코드 작성이의 의도를 파악할 수 없다. 

```js
function operateTime (inputs, operators, is) {
	
	inputs[0].split('').forEach((num) => {
	cy.get('.digit').contain(num).click();
	})

	inputs[1].split('').forEach((num) => {
	cy.get('.digit').contain(num).click();
	})
}
//1단계 
function operateTime (inputs, operators, is) {
	const [firstInput, secondInput] = inputs
	firstInput.split('').forEach((num) => {
	cy.get('.digit').contain(num).click();
	})

	secondInput.split('').forEach((num) => {
	cy.get('.digit').contain(num).click();
	})
}

//2단계 인자로 받을떄 바로 진행 

function operateTime ([firstInput, secondInput], operators, is) {
	firstInput.split('').forEach((num) => {
	cy.get('.digit').contain(num).click();
	})

	secondInput.split('').forEach((num) => {
	cy.get('.digit').contain(num).click();
	})
}
```

-> [[구조 분해 할당]] 활용해서 배열을 풀어서 명시적으로 사용한다. 

또다른 예시 
-> ```
```js
function formatDate(targetDate) {
	const date = targetDate.toISOString().split('T')[0];
const [year, month, day] = date.split('-');

return `${year}년 ${month}월 ${day}일`;
}

//리팩토링

function formatDate(targetDate) {
	const [date] = targetDate.toISOString().split('T');
const [year, month, day] = date.split('-');

return `${year}년 ${month}월 ${day}일`;
}

```

4. 유사 배열 객체
```js
const arrayLikeObject = {
0: 'hello',
1: 'world',
length: 2,
}

const obj= Array.from(arrayLikeObject);
```

유사배열 객체를 왜 알아야하지? 

- 대표적인 사례 [[arguments]]
	- 가변한 인자를 함수에 넘기고 있는데 매개변수가 없어도 잘 반환하고 있다. 
		```js
function generatePriceList() {

for (let i = 0; i < arguments.length; i++) {

const element = arguments[i];

console.log(Array.isArray(arguments));

console.log(element);

}

}

  

function generatePriceList() {

return Array.from(arguments).map((arg) => arg + "원");

}

console.log(generatePriceList(100, 200, 300, 400, 500));
		```
		-> for문으로 순회가 된다고 하면 map으로도 가능한건가? 
		-> 안된다. 유사배열이라 안됨.  
		-> 그럴떄는 Array.from으로 유사배열을 배열로 만들어야한다.
		-> 이렇게 되는 이유를 더 보면
		-> 유사배열은 배열과 같은 객체이고 for문으로 가능했던 이유는 유사배열이기에 순회가 가능했던 것 하지만 그 안에 프로토타입에는 고차함수가 내장되어있지 않아 사용이 불가능했던 것. 
		
- web API에서의 [[nodeList]]

5. **불변성** 
```js
const originArray = ["123", "456", "789"];

  

const newArray = [...originArray];

  

originArray.push(10);

originArray.push(11);

originArray.push(12);

originArray.unshift(0);

  

console.log(newArray);

console.log(originArray);
```

불변성을 지키기 위해 
1. 배열을 복사한다.
	-> 
2. 새로운 배열을 반환하는 메서드들을 활용한다.
	-> map, filter, slice, 


6. map vs forEach 차이 
```js
const prices = ["1000", "2000", "3000"];

  

const newPricesForEach = prices.forEach((price) => price + "원");

const newPricesMap = prices.map((price) => price + "원");

  
  
  

console.log(newPricesForEach);

console.log(newPricesMap);

  
  

//차이는 리턴값이 있으냐 없느냐

//왜 undefined? forEach은 주어진 요소를 돌리면서 callback으로 들어오는 함수를 실행시켜주는 것에 불과

//map은 매요소마다 반환된 값이 배열의 요소에 조작을 한다.

  

//배열의 요소에 맞게 함수를 실행시키려면 forEach를 사용하는게 맞다

//map은 새로운 배열을 만들때 사용한다.
```

7. Continue 와 break;
문의 흐름을 제어하기 위해 try catch 구문을 사용하는 것이 맞다. 
con


