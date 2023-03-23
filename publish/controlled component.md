
Up : [[knowledge_MOCs]]

출처 : 공식 문서 
저자 :
URL : 
인용 : 

## 정의 

React State를 "**신뢰 가능한 단일 출처**"로 만들어 두 요소를 결합할 수 있다. 그러면 폼을 렌더링 하는 React 컴포넌트는 폼에 발생하는 사용자 입력값을 제어한다. 이렇게 **React에 의해 값이 제어되어 입력 폼 엘리먼트를 제어 컴포넌트**라고 한다. 


### 신뢰 가능한 단일 출처
-> 하나의 상태를 나타내는 state는 한 곳에만 존재해야 한다. 
```html
<input type="text"/> // value = '주영' -> 신뢰 가능한 단일 출처라고 할 수 있지만

// 이 input의 value를 변수에 담아 사용하는 상황
value에 접근하려면 DOM과 JS의 변수 총 2가지가 존재 -> 두개의 출처가 되어버렸다.  


```

위의 두개의 출처로 인한 혼돈을 제어 컴포넌트로 해결 

## 사용법
```js
<form>
	<label>이름</label>
	<input
		type="text"
		value={name}
		onChange={(e) => {
		setName(e.target.value);
		}}/>
</form>
```

변경되는 input value가 매번 state로 push가 되어 Input의 value와 React의 value가 최신의 값으로 일치함이 보장되는 것 

## 특징
- 매 입력마다 State가 변경되어서 re-render이 일어난다.


## 요약
1. 리액트가 관리
2. state로 관리
3. 값의 신뢰성 보장
4. re-render 발생

## 차이
상태를 가지고 있는 것
데이터에 따라 Ui가 바뀌지 않는 것. 

### 생각의 연결고리
분야 :

키워드 

관련있는 메모 : [[form tag]]