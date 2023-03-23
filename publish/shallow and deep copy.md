

> 아는 것 :원시형과 참조형 간에 차이 
> 모르는 것: 

# 깊게 찾아본 계기 

배경: 클린코드 강의를 듣고 객체를 불변하게 다루는 방법에 대해 공부를 하고 있었습니다. 그러던 와중 얕은 복사와 깊은 복사의 차이를 내가 잘 모르는 구나를 깨닫게 됐고 찾아보기 시작했습니다.  그러던 와중에 어느 글에서는 얕은 복사와 깊은 복사의 차이가 동일한 참조값를 향유하고 있는가 이고 어느 곳에서는 복사되는 depth에 따라 차이를 불 수 있다라고 했다. 머리 속에서 충돌이 일어났고 내가 아는 것이 무엇인지 다시 점검해보려고 한다. 이글을 읽는 분들도 햇갈리셨더라면 이 글을 통해서 명확하게 이해할 수 있기를 원한다.

우선 얕은 복사와 깊은 복사를 이해하기 위해서는 역시 사전에 알아야하는 개념들이 있다.


## 서론 : 사전 지식
### 1. 자바스크립트: 원시타입과 참조타입인 [[자바스크립트 데이터 타입]]을 알아야한다.

- 원시형
	- undefined ,null, Boolean, Number, String,, Symbol
- 참조형
	- Object : new Object Array, Map, Set, Weak map, Date 
	- Function 

여기서 우리가 머리 속에 각인시켜야하는 것은 "원시형 타입은 불변하다" 입니다.
따라서 원시형을 복사할땐 걱정할 필요가 없습니다. 왜냐하면  원시형 데이터 타입은 불변하기에 값을 바꾸지 못한다. 만약 값을 바꾼다면 아예 새로운 메모리를 할당받아서 새로운 값을 만들기 때문입니다. 

그에 반해 참조형은 가변합니다. 참조형 타입은 새로운 값이 만들어지지 않고 직접적으로 변경이 가능합니다.!! 

원시형은 불변하고 참조형은 가변하구나... 를 먼저 알아야 그 다음 깊은 복사와 얕은 복사간에 차이를 더욱 명백히 이해할 수 있습니다. 

### 2. 참조형 타입의 객체나 배열을 조금 더 살펴보자 
```js
const array = [1,2,3]
const sameElementArray = [1,2,3]

console.log(array === sameElementArray) // false


const Object = {x : 1}
const sameElementObject = {x : 1}

console.log(Object === sameElementObject) // false
```

위의 예시를 통해서 다시 확인 할 수 있는 것은 원시형은 실제 값을 메모리에 적재하지만 참조형은 참조값을 저장한다는 것을 역으로 생각해보면 정확히 이해할 수 있습니다. 

위의 예시를 살펴보면 언뜻 보기에 동일한 요소들이 변수에 할당되어있기에 동일하다고 느껴질 수 있지만 참조형 타입은 참조값을 메모리에 저장하기에 객체나 배열 안에 있는 값의 동일 여부를 보지 않고 새롭게 만들어진 객체나 배열은 다른 것이라고 판단합니다. 

이 부분을 다시 한번 생각해보면 이후 얕은 복사를 더욱 잘 이해할 수 있습니다. 





## 본론 : 깊은 복사와 얕은 복사 정리

깊은 복사와 얕은 복사의 정의를 살펴보고 참조형 데이터 타입에 속한 배열과 객체를 불변하게 사용하는 방법을 살펴보겠습니다. 


그렇다면 참조형 데이터 타입에 속한 배열, 함수 ,객체를 불변하게 (원본에 영향을 끼치지 않도록) 사용하는 방법은 없을까요? 

그럴 때 알아야하는 개념이 오늘 알아볼 깊은 복사입니다. 

다양한 정의를 살펴보았지만 역시 MDN 정의가 가장 신뢰할 수 있었습니다. 

### 깊은 복사 
A **deep copy** of an object is a copy whose properties **do not share the same references** (point to the same underlying values)

동일한 참조값을 공유하지 않는다는 것이 핵심이며 더 쉽게 이해해보면 동일한 참조값을 공유하고 있지 않기 때문에 서로의 공간에서 값을 바꾼다고 할지라도 영향을 끼치지 않게 됩니다. 


### 얕은 복사
A **shallow copy** of an object is a copy whose properties share **the same references** (point to the same underlying values)

동일한 참조값을 공유하여 서로 같은 values를 가르키고 있습니다. 


여기서 잠깐!!! 
원시형 데이터 타입을 복사할 경우는???

```js
const string = 'hi '

let copiedString = string 

copiedString = 'bye'

console.log(string) // hi

```

원시형은 사전 지식 섹션에서 말했듯, 불변하다는 특징을 가지고 있습니다. 그렇기 때문에 서로 영향을 끼치지 않습니다. 다시 체크! 


### 객체의 복사를 알아보면
#### 1. Spread operator (ES6)
```js
const a = {
  en : 'Bye',
  de : 'Hi',
  text : 'text',
}

let b = {...a}

b.de = 'ju'
console.log(a.de) // 'Hi'

const c = {...a ,...b}

console.log(c)  // { en: 'Bye', de: 'ju', text: 'text' }
```

Q. 이부분이 제가 얕은 복사와 깊은 복사를 다르게 이해한 부분입니다. 얕은 복사는 한단계를 불변하게 복사하는 것이고 깊은 복사는 전체를 다 불변하게 복사하는 것이라고 지금까지 잘못 이해하고 있었습니다. 

```js
const a = {
  x : 'Hi',
  y : 'Hello',
  z : 'Sup',
}

let b = {...a}
```

A. 얕은 복사와 깊은 복사의 개념에서 잠시 잊고 가장 기초적으로 생각하니 되려 이해가 됐습니다. 왜 한단계만 복사가 되는지 이해가 됐습니다. 


우선 a라는 변수와 b라는 변수는 각각 다른 객체 입니다. 왜냐하면 object literal 방식으로 각각 다른 변수에 할당돼 서로 다른 메모리 주소를 가지고 있습니다. 그래서 현재 두개의 변수간에 영향을 끼치지 않는 상황입니다. 

하지만 만약 

```js
const a = {
  x : 'Hi',
  y : 'Hello',
  z : 'Sup',
  m : { a : 'bye'}
}

let b = {...a}
```

==새로운 객체인 b에 spread operator를 활용하여 a의 properties를 가지고 올 경우 원시형 데이터 타입은 복사가 될 경우 아예 새로운 값으로 변경되는 반면 우리가 위에서 배웠던대로 참조형 데이터 타입은 주소를 가지고 있기 때문에 서로 다른 두 객체 안에서 동일한 주소값을 가지고 있게 됩니다. 그래서 결과적으로 a,b의 x,y,z를 수정 혹은 삭제를 해도 서로 영향을 끼치지 않지만 m 을 삭제할 경우 서로 동일한 참조를 가지고 있기에 영향을 끼친다고 할 수 있습니다.==

즉 얕은 복사는 한단계만 복사한다. 깊은 복사는 전체를 복사한다는 설명은 현재 제 시각으로는 완벽한 정의는 아니다라고 생각합니다. 


#### 2. Object.assign
spread operator이 나오기 전에 가장 많이 사용됐던 방법

```js
const a = {
  en : 'Bye',
  de : 'Hi',
  text : 'text',
}

let b = Object.assign({},a)

b.de = 'ju'
a.de
```

#### 3. Pitfall : Nested Objects
중첩된 객체나 배열을 복사하면 중첩된 객체, 그 객체는 복사가 되지 않는다. 왜냐하면 중첩된 객체는 참조값만 가지고 있기 때문이다. (위에서 자세하게 설명했습니다. 햇갈리면 참고해주세요~ )

그래서 중첩객체를 deep copy(서로 다른 참조를 하도록) 하기 위해서는 수동적으로 모든 중첩 객체를 복사해주는 방법이 있습니다. 

```js
const a = {
  foods : {
  dinner : 'pasta'
}
}

let b = {foods:{...a.foods}}

b.foods.dinner = 'Soup'

a.foods.dinner
```


#### 4. 위의 같이 어렵게 하지 않고 쉽게 deep copy를 하는 방법

단순하게 객체에 stringify를 해주고 parse를 바로 해주면 어렵지 않게 객체의 모든 중첩된 객체까지 자동적으로 copy를 해줍니다.

```js
const a = {
  foods: {
    dinner: 'Pasta'
  }
}
let b = JSON.parse(JSON.stringify(a))

b.foods.dinner = 'Soup'
console.log(b.foods.dinner) // Soup
console.log(a.foods.dinner) // Pasta
```
[[객체의 복사]]









- Deep Copy 하는 법 
1. **모든 깊이에 있는 객체까지 복사하는 재귀 함수를 구현**

**2. JSON 사용**

**3. lodash의 cloneDeep() 사용**


- Mdn 정의 



얕은 복사의 정의가 동일한 참조값을 원본과 복사본이 공유하고 있다는 것인데 
```js
const array = {x: 1 }
const copy = array


// 왜? 얘는 한단계만 복사가 되는거지?
// spread 문법 때문인가?

const array = {x: 1}
const copy = {...array}

copy.x = 2

console.log(array)

// 깨닫게 된것
// 너무 얕은 복사, 깊은 복사, spread 문법에 함몰되어 있어 기본적인 것을 보지 못함
// copy = {...array}라는 것이 copy라는 변수에 새로운 객체 리터럴을 만들어줌으로써 아예 다른 메모리를 향유하게 되는 변수를 만들어준 것 그리고 그 안에 spread 문법을 활용해서 array에 있는 요소만 쓰윽 넣어준 것이기 때문에 요소 안에 있는 원시형은 불변하다는 특징때문에 당연하게 복사한 객체나 배열에서 값을 바꿔도 원본에 영향을 끼치지 않고 그 안에 참조형인 객체나 배열이 있을 경우 참조값만 가지고 있기때문에 copy에서 값을 바꾼다면 원본 array에도 영향을 미치게됨. 그래서 한단계만 불변하게 복사가 되는구나라고 정리할 수 있다.

//그렇다면 얕은 복사는 한단계만 복사하고 깊은 복사는 전체를 복사한다는 말은 올바르지 않다는 생각이 든다. 



```


얕은 복사(Shallow Copy)는 '주소 값'을 복사한다는 의미입니다. 얕은 복사의 경우 주소 값을 복사하기 때문에, 참조하고 있는 실제값은 같습니다. 

여기서 중점적으로 살펴본것이 왜 한 단계만 불변하고 두 단계서 부터는 가변하게 복사가 되는 것일까? 였다. 



#### 1. state 값이 배열일 경우
```js
1. let originArray = originArray.concat(newData)
    새로운 데이터를 기존 배열에 더해 새로운 배열을 만드느 방법 
2. Using Spread Elementes( ... )
```

ES5에서는 배열을 복사하기 위해 Slice 매소드를 사용했다

```js
const originArray = [1,2];
const copy = originArray.slice();

copy===origin // false


const originArray = [1,2];

const copy = [...originArray];

copy === originArray
```

둘다 얕은 복사를 하여 새로운 복사본을 생성한다고 한다. 한단계만 복사하는 것을 얕은 복사??

#### 2. state 값이 객체일 경우
```js

1. let tempObj = Object.assign({}, originObj)
//spread Property가 제안되지 이전에는 ES6에서 도입된 //Object.assign 메서드를 사용
4. let tempObj = JSON.parse(JSON.stringify(object));
5. ## Using Spread Elements ( … )

```


배열을 spread Operation하면 깊은 복사 -> 왜? 배열은 여러개의 값이 하나로 뭉쳐져 있기 때문에

객체는 spread Operation 하면 한단계만 깊은 복사 -> 원시값은 배열과 같이 깊은 복사 되지만 참조형 데이터 타입은 안됨 


[[Spread operator syntax]]

> 그럼 이건 복사가 아니구나?

```js
const obj = { 
  a: 'a',
  b: 'bd'
}

const obj2 = obj;
//이것도 복사라고 한다. 참조에 의한 전달 
//그럼 복사와 얕은 복사는 어떤 차이가 있는거지? 


console.log(obj2 === obj)
```

**메모리값을 같이 참조하고 있는지 아닌지가 핵심**

핵심

중첩 객체

-> 중첩 객체를 가지고 있으니 원본을 복사했을때 같은 참조값을 가지고 있어서 원복 배열에 영향 
-> 원본에 영향 x  







### 배열의 복사를 알아보면
자바스크립트에서는 배열은 객체입니다. 이번 블로그에서는 넘어가겠습니다~
우선 복사하는 여러가지 살펴보면

#### 1. spread operator
```js
const a = [1,2,3]
let b = [...a]

b[1] = 4

console.log(b[1]) // 4
console.log(a[1]) // 2
```

이부분이 나에게 미지수!!
Q. 얕은 복사는 한단계의 깊은 복사를 의미하는건가? 
-> 해결했습니다. 이게 제가 공부하면서 혼란스러웠던 것인데 위에 객체 복사하기 에서 설명을 했습니다. 


#### 2. 고차 함수 (map, filter, reduce)
세개의 메소드는 원본의 모든 요소들을 가진 새로운 배열을 반환하는 특징이 있습니다.  원본에 영향을 끼치지 않는 새로운 배열을 만들 수 있다. 

#### 3. Array.slice
```js
const a = [1,2,3]
let b = a.slice(0)
b[1] = 4
console.log(b[1]) // 4
console.log(a[1]) // 2
```

#### 4. Nested arrays 
객체와 마찬가지로 위의 3개의 방법으로 복사할 경우 배열 안에 있는 객체 혹은 배열을 복사하지는 못합니다. 얕은 복사만 가능하다고 합니다. 그래서 막기 위해 또 등장한 stringify -> parse 
```js
JSON.parse(JSON.stringify(someArray))
```

[[배열의 복사]]




### 출처
1. freeCodeCamp 공식 문서
https://www.freecodecamp.org/news/copying-stuff-in-javascript-how-to-differentiate-between-deep-and-shallow-copies-b6d8c1ef09cd/
2. MDN 공식 문서
https://developer.mozilla.org/en-US/docs/Glossary/Deep_copy
3. 모던 자바스크립트 e-book
4. Digital ocean
https://www.digitalocean.com/community/tutorials/copying-objects-in-javascript



## 관려있는 메모 
1. [[call by value]]
2. [[call by reference]]
3. [[데이터 타입에 의한 메모리 공간의 확보와 참조]]를 알아야한다. 
4. [[원시값과 참조형의 비교]]를 알아야 깊은 복사와 얕은 복사를 정확히 이해가능 
5. 리액트 : [[React.memo]] , [[useMemo]]
리액트 : [[얕은 비교]]





