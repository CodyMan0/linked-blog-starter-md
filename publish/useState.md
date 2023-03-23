
> state의 초기값을 정할 수 있고, return 값으로 state, setState를 돌려주는 hook

출처 : https://www.youtube.com/watch?v=RAJD4KpX8LA&t=454s


Q. **useState는 비동기인가?**
-> 배칭하는 곳에서는 비동기? 이후 commit은 동기? 비동기? 동기?

useState는 비동기가 아니다. useState는 동기적으로 작동하는 훅이고 컴포넌트가 렌더될 경우 즉시 실행된다.  

useState의 목적은 컴포넌트의 상태를 관리하도록 허락해주는 것이고 시간이 지나면 변하는 상태를 저장하고 업데이트해준다는 의미이다. useState는 두개의 value를 담은 배열을 리턴한다. 현재 상태와 업데이트 시켜주는 함수. state가 변경되면 컴포넌트는 리린더링이 일어나고 새로운 상태가 사용되어진다. 

여기서 중요한 것은 상태는 묶여 업데이트된다는 것. 이 말은 동일한 리렌더링때 여러개의 상태가 업데이트 업데이트되고 동일한 batch에 실행되면 state 업데이트는 동기적인 방법으로 업데이트가 되지만 리액트는 한번에 여러개의 업데이트를 수행하도록 설계되어있따. 실상은 한번의 랜더링 사이클에 업데이트와 프로세싱을 같이 한것일 뿐이다. 


- 사용 방법

```js
const [name, setName] = usestate(초기값)
```


```js
setAge(a => a + 1);
```
setState 함수에 callback 함수가 들어갈 경우 updater function으로 사용할 수 있다.  updater 함수는 pending state를 인자로 받아서 새로운 state return 한다. 여기서 중요한 것은 React가 Updater function을 **queue**에 넣고 컴포넌트를 리렌더링 시킨다는 것. 그래서 useState이 비동기아닌가? 라는 말이 나오는 것이 아닐까? 

다음 랜더링 동안 리액트는 queue 안에 있는 updater 함수의 이전 값을 최신 상태로 계산해준다. 

중요) useState은 동기적으로 사용되지만 React에서 업데이트 함수를 비동기적으로 설계해놓은건가? 

[[Updating state based on the previous state]]



- 내부 동작 코드 
```js
const useState = (initValue) => {
	let value = initValue;
	const setValue = (newValue) => {
	value = newValue
	}
	return [value, setValue]
}
```


setState 의 동작 원리
setState 4가지 동작 원리 
	1.  ==기존 컴포넌트의 UI를 재사용할 지 확인한다.==
	2.  함수 컴포넌트: 컴포넌트 함수를 호출한다 / Class 컴포넌트: `render` 메소드를 호출한다.
	3.  ==2의 결과를 통해서 새로운 VirtualDOM을 생성한다.==
	4.  이전의 VirtualDOM과 새로운 VirtualDOM을 비교해서 실제 변경된 부분만 DOM에 적용한다.

### 관련있는 메모
1. [[reconcilation]]

