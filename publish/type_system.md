
### 편집기 활용해서 타입시스템 확인하기

- fetch의 정의 
```ts
declare function fetch(input: RequestInfo | URL, init?: RequestInit): Promise<Response>;
```

참고 [[Promise (js)]]

-> 타입을 편집기에서 정의로 이동하기를 통해 찾아보는 것을 추천


### 타입이 값들의 집합이라고 생각하기 
지난번에 "타입은 값이다"가 햇갈렸는데 너 잘 만났다.


런타임 동안 **변수는 값**이 할당된다.
컴파일때는 **할당 가능한 값들의 집합**(TYPE의 범위)이 존재

-> 다른 팀원들
집합으로 이해하기?



타입 체커 이해하기 (집합 관점)
1. [[type_never]] (공집합)
2. 한가지만 포함하는 타입 : 유닛타입의 리터럴
3. 유니온 타입 ( " | ")(합집합)
--> 타입 체커는 집합의 관점에서 생각해보면 이해가 간다
==4. & 연산자  (교집합)
--> ("  &  ")==

#Q 왜 의미하는거지? 
-> A,b를가지고 있는 abc를 가지고 있어도 된다. 오류를 안잡는다. 필수 조건만 만족해라. -> 추상화와 관련 지난번 

[[구조적 타이핑]] 규칙들은 어떠한 값이 다른 속성도 가질 수 있다는 것을 의미 

```ts
interface Person {
name : string;
}
interface Lifespan {
birth : Date;
death? : Date;
}

type PersonSpan =  Person & Lifespan;
```

두 interface의 교집합이 없어서 never 같으나 타입 연산자는 인터페이스 속성이 아닌 타입의 범위 (컴파일때 할당 가능한 값들의 집합)에 적용되기에 Person, Lifesapn을 둘다 가지는 값은 인터섹션 타입에 속한다. (팀원들의 설명을 참고해서 이해해야겠다 )

```ts
const ps:PersonSpan = {
name : 'ju young',
birth : new Date ('1996/07/10')
death : new Date ('2088/07/10')
}
```

->& 말고 extends를 사용하면 더 일반적이다.

- 배열과 튜플 타입 '
```ts
const list = [1,2];
const tuple: [number, number] = list
```

관련있는 메모 : [[useState]]

```ts
function useState<S>(initialState: S | (() => S)): [S, Dispatch<SetStateAction<S>>];
```

[[tuple]]

타입 요약 정리 
![[스크린샷 2023-01-06 오후 4.03.00.png]]

### 타입 공간과 값 공간의 심벌 구하기 
타입 스크립트의 Symbol은 타입 공간이나 값 공간 중의 한곳에 존재한다라.........
우선 패쓰 
여기서 말하는 심볼이 자바스크립트 심볼을 말하는건가? 


#### 흩어진 지식 모음

1. 동일한 이름의 심볼과 값
- 똑같은 이름 하나는 타입 함수 
- instanceOf 는 런타임 연산자 === 값에 대한 연산을 한다는 것 === 타입은 런타임에는 없다.  함수를 참조하는 것. 

2. 식별자에 따른 심볼과 값
- type , interface 뒤에는 심볼
- const, let 뒤에는 값

3. 타입과 값 두 가지 모두 가능한 예약어
- [[Class]] 와 [[enum]]

![[스크린샷 2023-01-07 오후 12.27.53.png]]

값으로 쓰일때는 constructor가 생긴다. 


타입일때와 값일떄 다르게 동작하는 애들 
| 요소    | JS  | TS  |
| ------- | --- | --- |
| typeof  |     |     |
| this    |     |  subClass의 메서드 체인을 구현할떄 유용   |
| & , 1   |  AND OR   |  교집합, 합집합 타입 체커   |
| const   |  변수 선언   |  as const는 리터럴 또는 리터럴 표현식의 추론된 타입을 바꾼다.   |
| extends |  하위클레스에 사용   |  클래스 타입 제네릭 타입의 한정자를 정의 할 수 있다...    |
| in      |  for문에서 봤음   |  매핑된 타입에서 볼 수 있다.    |

- 타입스크립트 코드에서는 **타입의 공간**과 **값 공간**을 혼동하기 쉬움 
#Q 컴파일과 런타임인가? 
컴파일 -> 타입체커 
런타임 -> 값

-> 코드 작성시에는 코드와 값을 같이 쓰기에 혼동하기 쉬움 instanceof 예시! 



예시 ) 구조분해할당
```js
function email (option: {person : Person ...}){
// ...

}


function email ({person : Person ...}){
// ...

}
```

```ts
function email ({
person : Person
// 바인딩 요소 "Person"에 암시적으로 any가 할당
...}){
// ...

}
```

값의 관점에서 Person과 string이 해석되어서 라는데??? 
와닿지는 않음 음

-> 
```ts
function email ({
person...}: {person : Person, ...}){
// ...

}
```
타입과 값을 구분!! 


코드를 읽을때 타입인지값인지 구분하면서 코드를 작성해야한다. 









what is ?
->   TypeScript is **a strongly typed programming language that builds on JavaScript**


how to use ? 
-> typescript are annotated using `:TypeAnnotation` syntax


what do i decide ? 
-> after today's contents

what do i have not to use? 
-> after today's contents

### 타입 단언보다 선언하기
잉여속성체크가 되지 않기 때문에 
#흩어진지식 또한 타입 단언문을 사용할때에도 적용되지 않는다. 

1/10

**1/10 (화)**
### 객체 래퍼 타입 피하기 

자바스크립트 불변형 7가지
기본형은 메소드가 없는 특징을 가지고 있는데 
어떻게 string은 매소드가 있는거지? 

**자바스크립트에서 string에는 객체 메소드가 타입으로 정의 되어있다.** 
**-> 타입스크립트도 동일하다** 

다른 기본형에서 객체 래퍼 존재!
number -> Number
... 등등
!! 아하 Number이 객체 래퍼였구나? 그러니깐 매소드를 쓸 수 있는거였네 

**타입스크립트에서도 기본형과 객체 래퍼 타입을 별도로 지정한다.**
![[스크린샷 2023-01-10 오후 12.28.55.png]]
#### 결론
**오타 조심해라!** 기본형과 타입형 타입이 다르게 선언되어있다.
객체 래퍼 타입을 사용할 필요가 없고 기본형 사용하면 된다. 




### 잉여 속성 체크의 한계 인지하기
```tsx
interface Room {

	num : number;

	ceil: number;

}

  

const r : Room = {

	num : 1,

	ceil: 10,

	ele : 'pre'

} // 는 안되는데 



const obj = {

	num : 1,

	ceil: 10,

	ele: 10,

}

  

const r : Room = obj

```
Q. 두번째는 객체를 선언하고 그 객체를 변수에 할당해주니 [[구조적 타이핑]]이 먹힌다...??? 
-> 타입스크립트 잉여체크를 항상 해주는 것이 아니다?? 
-> 그 전 타입을 굳이 또 타입을 해줄 필요가 없도록 하려고? 

이유: obj 타입은 Room 타입의 부분 집합을 포함하고 있기때문에 타입 체커에서 통과?! 조금 이해가 될랑 말랑 

#### 두 예제간의 차이점.
첫번째 예제는 [[잉여 속성 체크]]라는 속성이 수행 , 할당 가능 검사 !== 잉여 속성 체크.



##### 타입 스크립트 타입 지정은 포괄적으로 지정도 가능하다
```tsx
interface Options {
title: string;
darkMode?: boolean;
}

const o1 : Options = document;
const o1 : Options = new HTMLAnchorElement;
```
document, HTMLAnchorElement 모두 string 타입인 title 속성을 가지고 있어서 할당문이 정상!! 아하 

##### 아직 흩어진 지식
#흩어진지식 객체 리터럴이 아니면 잉여속성체크가 적용되지 않는다.
#흩어진지식 또한 타입 단언문을 사용할때에도 적용되지 않는다. 

#### 요약
1. 객체 리터럴을 변수 할당 혹은 함수의 매개변수로 전달할때 잉여 속성 체크가 수행된다.
2. 잉여 속성 체크는 오류를 찾는데는 효과적이지만 일반적인 구조적 할당 가능성 체크와 다르다. 
	-> 뭐가 다른데!!!
3. 임시 변수를 도입하면 잉여 속성 체크를 건너뛸 수 있다.




### 함수 표현식에 타입 적용하기
**타입스크립트에서는 함수 표현식을 사용하는 것이 좋다.**

#Q why? 매개변수 부터 return값 까지 전체를 함수 타입으로 선언하여 표현식에 재사용할 수 있기에
-> 코드를 확인해보니 선언문은 인자를 무조건 할당해야한다. 
-> 형식이 다르다 
-> 눈으로 확인해보기 

#Q 선언문은 안되나? 동일하지 않나? 타입스크립트 함수 타입이 표현식 타입으로 정의되어있나? 

함수 타입 선언으로 중복되는 코드의 반복을 줄인다!
```tsx
function add (a:number, b : number) {return a + b};
function sub (a:number, b : number) {return a + b}
function mul (a:number, b : number) {return a + b}
function div (a:number, b : number) {return a + b}

->
type BinaryFn = (a: number , b:number) => number;
function add: BinaryFn(a, b ) {return a + b};
...
```

#흩어진지식 [[react MOC]]에서는 MouseEvent라는 타입 대신에 함수 전체에 적용할 수 있는 MouseEventHandler 타입을 제공한다. 


#### fetch 예시
```tsx
async function checkedFetch (input : RequestInfo, init?:RequestInt) {
const response = await fetch(input, init);
if (!response.ok){
	//거절된 프라미스
	throw new Error(res.status)
}
return res
}

--> 더 간결하게 타입 지정
const checkedFetch: typeof fetch = async(input, init) => {
	const res = await fetch(input,init);
	if(!res.ok) {
	...
	}
...
}
```

함수 선언문 => 표현식 함수 전체에 타입을 줬는데 함수 전체 타입은 뭐뭐가 지정되어있는거지? 

#### 결론
1. 함수 같은 경우는 매개변수에 타입을 지정하는 것보다 한단계 올라와서 함수 전체에 타입을 지정해주는 것이 간결하고 안전하다. 
2. 다른 함수의 시그니처를 참조하려면 typeof fn을 사용하면 된다. 아하!!

### 타입과 인터페이스의 차이점 알기
> 드디어!! 가보자고

타입스크립트에는 type을 정의하는 두가지 방식
1. **type**
2. **interface**

#Q. 클래스는 값으로 쓰일 수 있는 자바스크립트의 런타임의 개념? 혹시 이해되나요?  봐도 봐도 어색한 느낌

대부분은 type, interface 어떤 식별자를 쓰던 상관 없다. 
하지만 일관성을 유지하려면 기준이 있어야하고 결국 차이를 알아야 기준이 생긴다는 말을 한다.

#### 공통점 
우선 두 방식의 정의는 결과적으로 상태에는 차이가 없다. 
1. [[index signiture]] 모두 사용 가능
2. 함수 타입 정의 가능
3. 타입 별칭과 인터페이스는 모두 제네릭이 가능하다. 
	인터페이스가 타입을 확장할때는 ==조심==해야할 것이 있고 타입이 인터페이스를 확장할때는 자유롭다.

-> 조심할 부분
- 인터페이스는 유니언 타입같은 복잡한 타입은 확장하지 못한다. 그래서 &사용? 


#### 다른점
1. 유니온 타입  O  /  유니온 인터페이스 X 
	-> type 키워드는 유니온도 되고 매핑된 타입 또는 조건부 타입같은 고급기능에도 활용할 수 있지만 interface는 불가 
2. 튜플, 배열도 타입은 간결하게만들 수 있다. 
	```tsx
	// type
	type Pair = [number, number]
	type StringList = string[];

	// interface
	interface Tuple {
		name : string;
		capital : string;
	}
	const t: Tuple = [10,20] //작동은 하지만 매소드를 사용할 수 없다.
	
	```
3. 그렇다면 타입이 상위호환인 건가? 아니다 . interface에는 Type에 없는 기능이 있다.
	1) **arguments**
	```tsx
	interface IState {
	name: string;
	}
	interface IState {
	population: number;
	}
	

	const ju:IState = {
	name:'ju_young',
	population:500000
	}

	```

#### 사용 방법의 기준
1. 기존 타입에 추가적인 보강의 필요성 여부
2. 복잡하면 Type , 간단하면 interface 
3. API에 대한 타입 선언은 interface로 작성하는게 좋다. 하지만 타입 병합이 잘못될 수 있는 경우는 Type? 뭐야 이 작자!! 

#Q 보강과 typeScript 바벨과 연관이 있다. 


#### 결론
일관된 스타일을 사용하고 보강이 필요한지에 따라 결정 


**1/17 (화)**
### 타입 연산과 제너릭 사용으로 반복 줄이기
DRY 원칙에 대해 설명 -> 타입에 대해서 간과가능성 -

```ts
interface Person {
firstName: string;
lastName : string;
}

interface PersonWithBirthDate {
firstName: string;
lastName: string;
birth: Date;
}
```

타입 중복은 코드 중복 만큼 문제를 발생시킨다? 

**핵심** : 타입간에 매핑하는 방법을 익히면 타입 정의에서도 DRY의 장점을 적용할 수 있다.

#### 반복을 줄이는 방법
1. 간단한 방법 타입에 이름을 붙이는 것. 
-> 우리가 익히 사용하는 방법인데 상수를 사용해서 반복을 줄이는 방식으로 타입 시스템에도 적용한 것.
1-1. interface에서 공통적인 부분은 **extends**를 사용하거나 **&**을 통해서 확장 가능
```ts
interface Person {
firstName: string;
lastName : string;
}

interface PersonWithBirthDate extends Person {
birth: Date;
}

type PersonWithBirthDate Person & {birth : Date}
```

#Q. 이런 기법이 유니온 타입에 속성을 추가하려고 할떄 유용하다고 하는데 왜지?
-> 타입 확장을 유연하게 하려고 


```ts
interface State {
	userId: string;
	pageTitle:string;
	recentFiles: string[];
	pageContents:string;
}

interface TopNavState {
	userId : string;
	pageTitle: string;
	recentFiles: string[];
}
```

#Q 이것도 extends를 활용해서 타입을 정의하면 되지 않나? 왜 다른 방식으로 하지?
-> state의 부분 집합으로 TopNavState를 정의 -> State를 인덱싱하여 속성의타입에서 중복을 제거할 수 있다.
-> 논리적으로 생각하여 다시 정리 

```ts
type TopNavState = {
userId : State['userId'];
pageTitle: State['pageTitle'];
recentFiles: State['recentFiles'];
}

//여전히 중복된다고 한다

type TopNavState ={
[k in 'userId' | 'pageTitle' | 'recentFiles']: State[k]
}
```

이런식으로 인덱싱을 하면 무작정 중복된 타입을 지정했던 타입과 같이 동일한 정의가 표시되는 동시에 중복을 막을 수 있게 된다.

[[mapped type]]

#Q 제네릭 타입은 함수와 비슷하다? 


```ts
interface Options {
width : number;
height : number;
color : string;
label: string;
}

  

// interface OptionsUpdate {
// width?: number;
// height? : number;
// color? : string;
// label?: string;
// }

  

class UIWidget {

constructor (init: Options) {}

update (options : OptionsUpdate) {}

}

  

type OptionsUpdate = {[k in keyof Options]?: Options[k]};
```

==흩어져있는 지식 모음 (나중에 한데 모아 정리)==
**keyof**는 타입을 받아서 속성 타입의 유니온을 반환한다!!


- 값의 형태에 해당하는 타입을 정의하고 싶을때 
**typeof**
```ts
const INIT_OPTIONS = {
width: 640,
height: 480,
color: '1213',
label: 'VGA',
}

  

// interface Options {
// width: number;
// height: number;
// color: string;
// label: string;
// }

  

type Options = typeof INIT_OPTIONS
```

런타임의 연산자 typeof 가 아니라 컴파일 단계에서 연산되고 자스 typeof보다 더욱 정확하다고 한다. 

#Q 값은 런타임에 할당되는거 아닌가? 어떻게 값으로 부터 타입이 만들어지지? 

값으로 부터 만들어져서 선언 순서가 중요 타입 정의 -> 값이 그 타입에 할당 가능하다고 선언하는 것이 베스트

- 함수나 메서드 반환값에 커스텀하여 정의... ->  을 만들 수 있다.
-> 명명된 타입 : Options (타입 별칭)
-> 조건부 타입이 필요하다.  -> ReturnType 제네릭
```ts
type UserInfo = ReturnType<typeof getUserInfo>;
```

- typeof의 대상이 값인지 타입인지 알고 처리해야한다. 여기서는 타입! 


==흩어져있는 지식 모음 (나중에 한데 모아 정리)==
제네릭 타입은 타입을 위한 함수와 같다.


- summary
1. 타입 정의에도 DRY 최대한 적용
2.  이름을 붙여서 반복을 피하고 extends를 사용해서 interface의 필드의 반복을 피해야한다
3. 매핑을 위한 도구들 (keyof, typeof, indexing,  mappinged type) 공부하는 것 추천
4. 타입을 반복하지 않도록 제네릭 타입을 사용하여 타입들 간에 매핑을 하는것이 좋다. 
5. 표준 라이브러리 Pick, Partial, ReturnType 같은 제네릭타입에 익숙해지자.







### 동적 데이터에 인덱스 시그니처 사용하기
자바스크립트의 장점 중 하나 : 객체를 생성하는 문법이 간단하다
[[Advantage of JS]]
-> 자바스크립트 객체는 문자열 키를 타입의 값에 관계없이 매핑한다. 
의미 : 


```Ts
type Rocket = {[property: string]:string}

const rocket : Rocket = {

name : 'Flcon',

variant: 'df',

thrust : 'sdfds'

}
```

`[property: string]:string` 가 인덱스 시그니처고 세가지 의미를 담고 있다.

1. 키의 이름: 키의 위치만 표현하는 용도
2. 키의 타입: string 혹은 number 또는 symbol의 조합이어야 하지만 보통 string을 사용한다
3. 값의 타입 : 어떤 것이든 될 수 있다.

위의 방식대로 타입 체크가 수행되면 단점 4가지
1. 모든 키 허용
2. 키가 필요하지 않은 것
3. 동일한 타입 요구
4. 자동완성 사용 불가

위에서 본 인덱스 시그니처는 부정확해서 인터페이스 사용해야한다. 그럼 인덱스 시그니처는 언제 사용해야하는거지?
-> **동적 데이터**를 표현할때 -> 동적 데이터가 뭔데? (계산되고 가공되는 데이터) -> 언제 사용되는데?(서버에서 실시간으로 변환되어 적용이 될떄 사용됨 ) 
-> 서버 데이터는 스키마를 알기에 동적 데이터가 아니다. 왜냐하면 스키마가 있으니깐 (영준)
-> 추가적으로 타입을 확장시키고 싶을떄 사용했던 것 같다 (태희)

-> 객체의 키값을 미리 알 수 없을때 사용하는 방식이라는 것 같다. 

인덱스 시그니처를 사용하지 않아야할떄 -> 타입이 정의되지 않고 제한되어있을때 
사용할떄 -> 타입의 범위가 포괄적일때? 
-> 인덱스 시그니처 사용시 에러가 많이 나옴.
-> ==안쓰는게 답이다.==

- 요약
1. 런타임까지 객체 속성을 알 수 없을떄 인덱스 시그니처 사용
2. 안전한 접근 위해서 시그니처 값 타입에 | undefiend 추가 고려
3. 정확한 타입 선언 사용 권장

### number 인덱스 시그니처보다는 Array, 튜플, arrayLike 사용하기
[[limitation of JS]]
자바스크립트에서 객체는 key/value의 모음
- 객체의 키값으로는 숫자와 객체를 사용할 수 없다.
- 배열의 타입은 객체 
```js
x = [1,2,3]
x[0] // 1

x['0'] // 문자열이어도 값이 나온다.

let x = [1,2,3]
console.log(Object.keys(x)) /// [ '0', '1', '2' ]
```

위의 문제를 해결하기 위해 타입스크립트는 숫자를 키로 허용하고 문자열 키와 다른 것으로 인식하다.

92Page 너무 어렵다.

### 변경 관련된 오류 방지를 위해 readonly 사용하기 
**1/27**
### 매핑된 타입을 사용하여 값을 동기화하기
특정 인터페이스 또는 타입의 property들과 동기화된 새로운 타입을 재생산 하려면 '매핑된 타입' 기능을 사용하면된다.

아래 예제는 사용자 계정 정보를 표현하는 인터페이스를 정의하였고, 사용자 정보 중 일부 property만 업데이트 하기 위한 flag object를 생성하고 있다.


// 사용자 계정 정보를 표현하는 인터페이스 타입
```ts
interface UserAccount {

    email: string;

    nick_name : string;

    password: string;

    age : number;

    readonly sign_in_date : Date;

    info: string;

}

  

//UserAccount 같은 타입의 특정 property를 업데이트 하기 위한, 업데이트 flag 자료구조를 구성하기 위한 방법은?

const USER_ACCOUNT_UPDATE_FLAGS: { [k in keyof UserAccount]: boolean } = {

    email: false,

    nick_name : true,

    password: true,

    age : false,

    sign_in_date : false,

    info: false

}

```

위와 같이 [k in keyof T]: type 을 이용하여 동기화된 매핑 타입을 정의할 수 있다.
### 추론 가능한 타입을 사용해 장황한 코드 방지하기 

저자의 의견 

고수 : 반드시 필요한 부분에만 타입을 명세해 주는 노하우를 가지고 있다. 타입 명세를 난발하지 않아 코드가 장황하지 않다.

하수 : 굳이 필요없는 타입 명세를 명시적으로 계속해서 코드가 장황해진다.



함수 파라미터로 object를 할당받았을 때, 각각의 property에 대한 값 취득 시 비구조화 할당 문을 사용하면 타입을 명시하는 것보다 더 편리하다. 
```ts
interface Product {

    id: number;

    name: string;

    price: number;

}

  

function logProduct(product: Product) {

    const id: number = product.id;

    const name: string = product.name;

    const price: number = product.price;

    console.log(id, name, price);

}

  

function logProductFix(product: Product) {

    const {id, name, price} = product;

    //typeof id = number;

    //typeof name = string;

    //typeof price = number;

    console.log(id, name, price);

}
```

**-> 비구조화 할당문은 타입추론을 해준다**

위와 같이 저자는 이상적인 타입 스크립트 코드는 함수 혹은 메서드 구현부에 타입 구문을 포함시키고, 함수 내 로컬 변수 할당 시 티입 구문을 일일이 명시하는 것은 불필요하다고 주장한다. 함수를 읽는 사람에게 로직에 대한 이해만 잘 될 수 있도록 집중시키는게 그 이유라고 한다.


다음으로, 타입 체커에 의해 타입이 추론 가능한 상황임에도 불구하고 타입을 명시하고 싶은 상황에 대해 고민해보자.

그 상황 중 하나로 객체 리터럴을 정의할 때가 될 수 있는데, 잉여 속성 체크 기능의 도움을 받는 상황이라 할 수 있다.



이밖에, **함수의 리턴 타입에 타입을 명시**하면 미리 오류를 방지하는데 도움이 된다.




### 다른 타입에는 다른 변수 사용하기 
자바스크립트를 사용할 때, 하나의 변수를 다른 목적으로 재사용 한 경험이 있는데 이 경험을 그대로 타입스크립트에 적용을 해보면 아래와 같은 문제가 발생한다.

let temp = "aaa-bbb-ccc"; // 타입 추론에 의해 temp의 type은 string;

console.log(temp);

  

temp = 1; // 에러 발생 : temp 의 type은 string이기 때문에 number를 대입할 수 없음.

위 사실에서 우리는 ==변수의 값은 바뀔수는 있으나 최초 정해진 타입은 보통 바뀌지 않는 다는 사실==을 알 수 있다.

타입을 바꿀수 있는 상황은 기존 타입의 범위를 확장 하는게 아니라 **좁히는(Narrowing) 상황**으로 제한적이라고 한다.

위 예제를 뜯어 고치려고(한 변수를 다른 목적으로 굳이 사용하려고) 유니온 타입을 활용할 수 도 있는데, 이와 같은 접근 방법은 타입 체커나 코드를 읽는 사람 모두에게 혼란을 야기한다. 

다른 타입에는 별도의 변수를 할당하는게 바람직하다고 하는데 그 이유들은 다음과 같다고 함.

* 변수명을 더 구체적으로 명시할 수 있어서 가독성 향상.

* 타입 추론을 향상, 타입을 구별하기 위한 코드내 분기문 난발 방지.

* let 대신 const로 변수를 할당하기에 더 유리하고, const로 변수를 할당하면 더욱 strict한 타입 체킹을 유도할 수 있다.
### 타입 넓히기 
타입 스크립트의 '타입'이라는 개념은 타입을 체크하는 정적 분석 시점에서, 할당 가능한 '범위'로 이해할 수 있다.

'타입'이란, 할당 가능한 값들의 '집합'의 개념인 것이다.

상수를 사용해서 변수를 초기화할 때, 타입을 명시하지 않으면 타입 체커는 타입을 결정한다. 다시 말해, 지정된 단일 값을 가지고 할당 가능한 값들의 집합(타입)을 유추한다는 뜻이다. 여기서 '유추'하는 과정을 **넓히기(Widening)**이라고 부른다. 넓히기 과정을 이해한다면 오류의 원인을 파악하고 타입 구문을 좀 더 효과적으로 사용할 수 있다고 한다.

아래의 예제를 보면서 타입 채커가 타입 넓히기를 어떻게 하고, 타입을 유추하는지 알아보도록 하자.
```ts
interface Vector2 {

    x : number;

    y: number;

}

  

const getComponent = (vector: Vector2, axis: 'x' | 'y') => {

    return vector[axis]

}

  

const vector: Vector2 = {

    x: 3,

    y: 4

}

  

let x = 'x'; // 타입 추론에 의해 x 의 타입은 string;

console.log(getComponent(vector, x)); // 'x' | 'y' 파라미터로 허용하는 함수에 string 타입과 함께 호출시 에러가 발생.  
  

//넓히기 과정을 제어할 수 있는 한가지 방법으로 const 로 변수를 선언하는 것.

const y = 'y'; // 타입 추론에 의해 x 의 타입은 'y';

console.log(getComponent(vector, y)); //정상
```

하지만 const 로 타입을 넓히는게 만능이 아니다. 


타입 추론의 강도를 직접 제어하기 위한 3가지 방법이 있다고 한다.
1. 명시적 타입 구문을 제공하는 것 
2. 타입 체커에 추가적인 문맥을 제공하는 것
3.  const 단언문을 활용하는 것
```ts
const v1 = {

    x: 1,

    y: 2,

} // 타입은 {x : number; y: number;}

  

const v2 = {

    x: 1 as const,

    y: 2,

}; // 타입은 {x: 1; y: number;}

  

const v3 = {

    x: 1,

    y: 2,

} as const // 타입은 { readonly x: 1; readonly y: 1;}

//as const로 명세하면, 타입스크립트는 최대한 좁은 타입으로 타입을 추론한다.

const a1 = [1, 2, 3] // 타입이 number[];

const a2 = [1, 2, 3] as const // 타입이 readonly number [1, 2, 3];
```