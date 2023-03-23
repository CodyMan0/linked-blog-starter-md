

## 사전 개념 정리 🔍
> 1. spread 문법 :spread 라는 단어가 가지고 있는 의미는 펼치다 그리고  퍼뜨리다 입니다. 이 문법을 사용하면, 객체 혹은 배열을 펼칠수있습니다. 또한 기존의 배열을 건드리지 않으면서 개로운 내용을 넣을 수 있게 된다. (깊은 복사)
> 2. 얕은 복사 : **동일한 주소를 참조**하어 original의 객체 혹은 배열에도 영향을 끼치는 복사.
> 3. 자바스크립트 안에서 참조 값: 원시타입이 아닌 값(non-primitive value)이 할당된 변수들은 그 값으로 향하는 참조 값(reference)를 갖게 된다. 참조 값(reference)는 메모리에서의 객체의 위치를 가리키고 있다.


## 왜 리액트의 useState hook을 이용하여 배열과 객체를 사용할 때 spread 문법)으로 깊은 복사를 해야하는거지? 
아래 예시를 보면 댓글을 등록하면 그 전에 있는 모든 댓글들 위에 나의 댓글이 쌓이게 하고 싶었다. 그래서 찾아보다가 "그 전에 있는 모든 댓글 위에" 를 구현하고 싶어서 const pot = [comments] 를 하였는데... 동작할 생각을 하지 않았다. 그래서 찾다가 알게 된 것이 '배열과 객체는 spread 문법을 사용해서 활용해야하는구나' 였다. 

그렇다면 여기서 why❓  를 짚고 넘어가보자

``` Jsx
const registerComment = e => {

e.preventDefault();

const pot = [...comments];

pot.push(value);

setComments(pot);

setValue('');

};
```

위위 부분을 정확히 이해하기 위해서는 두 단계를 생각해볼 수 있다.

첫번째, 자바스크립트 안에서 배열과 객체가 어떻게 데이터를 저장하는지를 알아야 이해할 수 있다는 것을 알게 됐다. (하.. 하나 알고 싶어서 들어왔다가 수 십가지의 개념을 알아갈 수 있어서 기쁘지만 녹록치 않다!!)

자바스크립트에서 객체와 배열은 참조값만 저장되고 실제 데이터는 RAM 어딘가..(아직은 모르겠다)에 저장된다. 

```
let array = [1,2,3,4]

let array1 = array // array 1과 array 는 동일한 참조값을 가지고 있다.


```

**객체와 배열은 참조값으로 데이터를 가지고 있다.** 

리액트를 한 문장으로 정리하자면 

리액트는 SPA이며 가상돔을 활용하여 **변화된 부분**을 계산을 해주어 자동으로 UI를 업데이트 시켜주는 아주 편리한 라이브러리!

여기서 변화된 부분을 useState라는 리액트 내장 매소드를 통해 알 수 있다.

- useState의 동작 원리를 살펴보자면 

`const [state(초기값), useState] = useState(초기값)`

``` jsx
function useState(init){
	let state = init;
	function setState(value){
	state = value}
	return [state, setState]
}
```
🗄😀😅
초기 값이 들어오면 state에 초기값을 할당해주고 setState에 새로운 value가 들어오면 state를 업데이트 시켜주어 업데이트된 state와 업데이트 함수를 배열 안에 반환해주는 hook이다. 

-  state 변경 함수의 특징
들어온 인자로 기본 state 값을 갈아치워준다. 하지만 한가지 조건은 **기존 state와 비교해서 같으면 변경해주지 않는다는 것**. 

동작원리와 setState의 특징을 살펴보았으니 이제 블로그의 주제로 돌아가서 왜 setState안에서 state를 받아올때 그 state가 배열일경우 spread 문법을 사용해서 가져와야하는지를 생각해보고자 합니다.

객체와 배열은 참조값을 가지고 있으며 위에서 봤듯 let array1 = array이라고 복사를 했음에도 새로운 배열을 만든 것이 아니라 동일한 참조값을 소유하고 있습니다.  동일한 참조값이니 setState는 동일한 값으로 판단해서 UI를 업데이트 해주지 않는 것이었다.  


자바스크립트의 기본 개념이 리액트와 연관이 있을 줄이야.. 




참고자료
- https://learnjs.vlpt.us/useful/07-spread-and-rest.html
- https://woo-dev.tistory.com/43


### 관련있는 메모
[[Javascript]]