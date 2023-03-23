

출처 : gitNation
저자 : ILLIA KIBALNYU
URL : https://portal.gitnation.org/contents/generic-components-with-ts-and-react
인용 : 




# React에서 TS를 활용한 generic component 만들기 

## Generic Component란
데이터만 넣으면 어디서든 쓸 수 있는 컴포넌트를 말합니다. 예를 들어, DropDown, select, Form 그리고 Field 컴포넌트 등이 있습니다.

그렇다면 Typescript를 활용하여 generic component를 만들기 위해서 알아야하는 선수 지식이 뭘까요?

## Generics (사전 지식)
소프트웨어 엔지니어링에서 중요한 요소는 컴포넌트를 APIs를 사용하는데 있어 잘 설계하는 것도 중요하지만 어떠한 데이터에를 넣어도 재사용이 가능한 컴포넌트를 만드는 것이라고 합니다. 이러한 측면에서 타입스크립트를 사용할때 기본적인 문법이 제네릭이라고 합니다.

함수를 선언해주고 다양한 곳에서 재사용한다고 가정해보겠습니다. 공식 문서의 예시를 가져왔습니다. identity 함수에 number 타입 변수를 지정한다면 호출하여 사용할때 number 타입만 받을 수 있기에 재사용하는데 불편함을 느낍니다. 그렇다면 어떻게 할까요? 

```ts
function identity(arg: number): number {
	return arg;
}

//호출부 
identity(5) // success
identity('hi') // error!! 
```

any 타입을 지정해서 어떤 타입도 파라미터로 받을 수 있는 함수를 만들어 재사용할 수 있게 해야하는 걸까요? 

```ts
function identity(arg: any): any {
	return arg;
}

//호출부 
identity(5) // success
identity('hi') // success
```

이것도 하나의 방법일 수 있겠지만 파라미터의 타입을 알 수 없어지기 때문에 타입 시스템의 이점을 활용할 수 없다는 의미일 수도 있습니다. **그래서 우리가 사용해야하는 것은 제네릭 타입 변수입니다.** 


```ts
function identity<T>(arg: T): T {
	return arg;
}

//호출부 
identity<number>(5) // success
identity<string>('hi') // success
```

위의 예시와 같이 identity함수에 T라는 제네릭 타입 변수를 더하면 함수가 호출된 시점의 타입을 받아서 identity 함수를 재사용할 수 있습니다. 위에서 봤던 any 타입과는 다르게 제네릭 타입 변수를 사용하면 파라미터와 리턴 타입 정보를 잃지 않습니다. 

위에 호출부에서 사용했던 코드를 살펴보겠습니다. 제네릭 함수를 재사용할때 <>안에 해당하는 타입을 꼭 선언해야할까요? 선언해도 되지만 타입스크립트의 타입시스템이 추론을 해준다고 합니다. 그래서 간단한 타입의 인자가 들어갈 경우에는 생략이 가능하지만 복잡해질 경우엔 타입 추론을 하기 쉽도록 타입을 지정해주는 것이 좋다고 합니다. 

```ts
identity(5) // success
identity('hi') // success


// 복잡한 인자 
type = {
a: string[],
b: 복잡한 인자의 객체 [],
...
}

identity<복잡한인자타입>(복잡한 인자) // success
```



### 제네릭 타입을 사용하는 이유
제네릭은 **선언 시점**이 아니라 생성 시점에 타입을 명시하여 하나의 타입만이 아닌 다양한 타입을 사용할 수 있도록 하는 기법이다. 한번의 선언으로 다양한 타입에 재사용이 가능하다는 장점이 있습니다.

다시 말해 제네릭 타입인 함수의 정의부에서 타입이 지정되는게 아니라 호출된 시점에 들어간 타입에 따라 다양한 타입을 사용할 수 있도록 하는 방식이라고 이해할 수 있을 것 같습니다. 

### 제네릭의 제약
위에 있는 identity 함수를 보면 

```tsx

function identity<T>(arg: T): T {
console.log(text.length) // 여기서 text.length의 타입은 지정되어있지 않기 때문에 에러가 에러가 발생합니다. 
	return arg;
}

```

그래서 제네릭 타입에 직접 타입을 지정할 수 있습니다.

```tsx
function identity<T>(arg: T[]): T[] {
console.log(text.length) // success
	return arg;
}

```

이렇게 제네릭 타입 변수를 지정할 수도 있지만 <> 안에서 추론을 도와줄 수 있는 방법도 있습니다


```tsx
interface LengthWise {
  length: number;
}

function identity<T extends LengthWise>(arg: T): T {
console.log(text.length) // success
	return arg;
}
```

class 문법의 extends와 비슷하게 사용할 수 있습니다. 제네릭 함수 안에서 LengthWise라는 인터페이스를 받도록 설정하여 제네릭 타입 변수(text : T) 에서 변경하지 않고 함수 내에서 해결 할 수 있게 됐습니다. 

## TS를 활용하여 react component 만들기 

데이터에 따른 드롭다운을 구현해보려고 합니다. 
![[야채.excalidraw.png]]

```

```





### 참고 자료
1. 타입스크립트 핸드북 : https://joshua1988.github.io/ts/guide/generics.html
2. 타입스크립트 공식문서 :https://www.typescriptlang.org/docs/handbook/generics.html



### 생각의 연결고리
분야 :

키워드 :

관련있는 메모 :
