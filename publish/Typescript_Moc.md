
- typescript 연습 페이지  : [playGround](https://www.typescriptlang.org/play?#code/JYWwDg9gTgLgBAbzgVwM4FMCKz1QJ5wC+cAZlBCHAORToCGAxjALQCOO+VAsAFCiSw4dAB7AIqUuUpURY1Nx68YeMOjgBxcsjBwAvIjjAAJgC44AO2QgARriK9eDCOdTwS6GAwAWmiNon6ABQAlGYAClLAGAA8vtoA2gC6AHx6qbLiAHQA5h6BVAD02Vpg8sGZMF7o5oG0qJAuarqpdQ0YmUZ0MHTBDjxOLvBInd1EeigY2Lh4gfFUxX6lVIkANKQe3nGlvTwFBXAHhwB6APxwA65wI3RmW0lwAD4o5kboJMDm6Ea8QA)

자바스크립트는 동적 타입 언어이다.  즉 **런타임**에 실제 코드의 값이 평가 될 시점에서야 이 변수에 들어올 값과 타입을 알 수 있다는 뜻인데

반면 **정적 타입 언어**들은 **컴파일되는 시점**에 변수의 타입을 결정한다. 그러니 굳이 실제 코드를 실행해보지 않더라도 이 변수의 값이 무슨 타입인지 **빌드 타임**에 미리 알 수 있다.

## Why use?
1. 코드의 흐름을 알려줌
2. 에러를 런타임 이전에 알 수 있어 개발 경험에 좋다

## 구성 요소
1. 언어 선택 : 유형, 키워드 및 구문에 대한 주석이 포함된다. 
2. 컴파일러 : JS로 변환된다,
3. 언어 서비스  : 컴파일러 프로세스 위에 두번째 계층으로 편집기와 같은 앱을 제공한다. 

## TS 특징
- 자바스크립트와 관계 : [[relation with TS and JS]]
- 타입스크립트의 목적 : [[purpose of TS]]
- 타입스크립트 컴파일러 : [[Typescript compiler]]
- 타입스크립트를 사용하는 진정한 이유 : [[type_system]]

## 학습
강의 : [[typescript udemy]]
원티드 세션 : [[typescript session]]
스터디 : [[typescript_study]]


## 간단한 내용
1.  객체 타입 검사용 : satisfies 연산자
```ts
const palette = {
	red: [255, 0, 0],
	green: "#00ff00",
	bleu: [0, 0, 255], // blue 오타 
} satisfies Record<'red' | 'green' | 'blue', [number, number, number] | string>;
```
포인트 : 트랜스파일러, 컴파일러, 파싱, 바벨


### 생각의 연결고리
분야 :

키워드 :

관련있는 메모 : [[webPack]], [[programming Moc]]