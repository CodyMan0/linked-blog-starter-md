공식 문서 : https://kit.svelte.dev/docs/introduction
참고 문서 : https://heropy.blog/2019/09/29/svelte/
[[svelte working process]]

## 주제 : svelte
브라우저에 실행될떄 하는 모든 과정을 사이트가 배포 되기 전에 미리 다 해둔다. 하지만 생긴지 별로 안됐기 때문에 기능이나 커뮤니티가 덜 쌓인 부분들이 있다.

## Svelte란
리액트와 뷰와 다르게 프레임워크 혹은 라이브러리가 아니라 컴파일러에 가깝다. 스밸트가 JS 코드로 브라우저가 이해할 수 있도록 컴파일을 해준다. 그래서 프레임워크 혹은 라이브러리를 다운로드할 필요가 없다. 그렇게 되면 SPA인 Svelte는 소스코드를 브라우저가 렌더링을 할떄 HTML을 받아오고 CSS와 JS를 받아온다. 그때 JS가 타 라이브러리보다 가볍기에 빨리 로드되고 결과적으로 TTV(유저가 화면을 보는데 걸리는 시간)이 축소돼 SPA의 단점을 보완한게 아닐까 생각이 든다. 


## 리액트와 뷰와 차이
리액트와 뷰는 우리로 하여금 선언적인 코드를 작성할 수 있도록 도와줬으나 많은 패널티가 있었다. Dom에 변경 사항을 반영하기 위해 추가적인 작업(diffing)을 요구 했던것. 그로 이냏 비용과 GC의 부과적인 일이 요구됐다. 대신 스벨트는 빌드 타임에 운영된다. 그래서 선언적으로 작성한 컴포넌트를 효과적으로 명령형 코드로 변환해준다. 그 결과 엄청난 성능의 어플을 만들 수 있게 됐다. 

스벨트는 컴파일러이기 때문에 뒷단에서 우리가 모르는 일을 해준다.
```ts
//스테이트를 만들면 
count += 1 

//컴파일러는 코드를 이렇게 해석한다
count += 1; $$invalidate('count', count)

```


## Virtual DOM 복습하기 
리액트 : render( ) 함수안에서 JSX 문법으로 작성되고 props or State 가 바뀌었을때 reconcile이 일어난다. 가상돔때문에 성능이 빠르다는 것은 거짓부렁까지는 아니지만 확실한 것은 아니다. 그래서 svelte는 가상돔 자체를 쓰지 않는 방법을 채택.


## Svelte 태그 사용법 
1. script : 상단에 script 태그 삽입시 자바스크립트 혹은 타입 스크립트를 사용할 수 있다.
2. style : style 태그 삽입시 css 스타일링이 가능하다.
3. HTML : 하단에 HTML 태그를 작성하면 끝. 



##  강의에서 나온 스벨트 개념 정리 

### state
스벨트에서 state(DOM 업데이트를 trigger하는 값)를 만들기가 간편하다.
```ts
let count = 0 
//리액트보다 간편하다. 그저 변수에 값을 할당만 해주면 된다.
```

### props 사용 
1. 자식이 Props를 사용하기 위해선 자식 컴포넌트에 아래 코드를 작성하면 된다. 
```js
export let props;
```

2. 받은 Props의 값을 default로 설정하기 위해선.
```ts
// Parent.svelte
<Children>

// Children.svelte
<script>
	export let answer = 'a mystery';
</script>

	<p>The answer is {answer}</p> 
// 상위 컴포넌트에서 Props를 넘기지 않으면 Default 값이 들어간다.

// The answer is 'a mystery'
</script>
```

3. 객체인 스테이트를 props로 내려줄때는 spread 연산자를 사용할 수 있다.

4. 데이터를 수정할때 , props를 그대로 받아서 view에 뿌려주지 않고 객체에 프로퍼티에 재선언을 해줘 값을 불변하게 만들어줘! 수정하다 취소를 눌렀을때 수정한 값이 반영되지 않도록 진행한다. 

### 반응성
값의 할당(assignments)만으로 업데이트를 트리거가 된다. 리액트에서는 setter(setState)가 필요했다. 

### 라우터 
tinro를 라이브러리를 사용하고 있다. 리액트에서는 react-router-dom을 사용한다
중첩 라우팅도 되고 fallback 기능을 활용해서 not-Found 페이지 라우팅도 된다. 

```js
<script lang='ts'>
  import { Route } from 'tinro';
  ... 생략
</script>

<Route path="/" redirect="/articles/all" />
<Route path="/articles/*">
//중첩 라우팅이 가능하다.
  <Route path="/all/*"><Articles /></Route>    
  {#if $isLogin}
    <Route path="/my/*"><Articles /></Route>
    <Route path="/like/*"><Articles /></Route>
  {:else}
    <Route path="/my/*" redirect="/articles/all" />
    <Route path="/like/*" redirect="/articles/all"><Articles /></Route>
  {/if}
</Route>
<Route path="/login"><Login /></Route>
<Route path="/register"><Register /></Route>
<Route fallback><NotFound /></Route>  
//fallback 기능이 있다. 해당하는 url을 찾지 못하면 fallback 라우터를 실행한다.

```


### 강의 아키텍처
1. 실제 서버와 통신하는 여러 함수의 공통적인 부분을 service / api.js에서 모듈화 하여 사용하고 있으며 그 모듈을 사용하기 위해 해당 모듈 아래에서 함수를 만들어 참조하고 있다. 다른 컴포넌트에서 get,post,put,delete를 서버에 요청하고 싶을때 모듈을 사용하는 것이 아닌 모듈을 참조하고 있는 함수를 사용하면 되도록 설계하심. 


### 마크업으로 비동신 처리 
예시) 공식문서 
```ts
{#await promise}
	<p>...waiting</p>
{:then number}
	<p>The number is {number}</p>
{:catch error}
	<p style="color: red">{error.message}</p>
{/await}
```

예시) 인프런 강의

최상위 컴포넌트에서 
```js
// main.js
await auth.refresh(); // 여기서 await을 해서 호출해도 정상작동하기는 함
```

최상위 바로 밑 컴포넌트에서 
```js
//App.svelte
<div class="main-container">
  {#await auth.refresh() then}
    <Router />  
  {/await}
</div>
```

-> 둘다 정상 작동 
auth 스토어에서 refresh 함수의 결과값이 True 일때 그때서 Router 컴포넌트를 실행시키겠다는 의미!! 즉 refresh 토큰에 의해서만 라우터가 이동될 수 있게 만드는 것. 

### Derived 
이미 만들어진 스토어를 기반으로 새로운 리턴값을 만드는 스토어, 불변하다는 특징을 가지고 있다.  또한 **비동기적**으로 작동한다.

```js
//app.svelte
<script>
	import { name, greeting } from './stores.js';
</script>

<h1>{$greeting}</h1>
<input bind:value={$name}>


//store.js
import { writable, derived } from 'svelte/store';

export const name = writable('world');

export const greeting = derived(
	name,
	$name => `Hello ${$name}!`
);
```

### 스토어
#### writable 함수의 내장 매소드
1. subscribe(구독)
2. set
3. update

```js
const {subscribe , set , update} = writable(something)
```

#### 값 사용 함수
1. get : 다른 스토어에서도 값을 참조하는 경우에 사용되거나 일반 자바스크립트 파일에서 store 값을 가지고 올떄는 무조건 get 

### 라이프 사이클 함수
1. onMount  
```js
  onMount(async () => {
    const onRefresh = setInterval(async () => {
      if($isRefresh) {
        await auth.refresh()
      }
      else {
        clearInterval(onRefresh)
      }
    }, refresh_time)
  })
```
fetch는 onMount 함수 안에서 사용하는 것을 권장.

2. onDestroy (컴포넌트가 unMount될 때)
setIntervel과 같은 비동기 함수로 인한 메모리 누수를 막기 위해 사용된다. 

3. beforeUpdate
state 값이 할당되어 돔이 변경되기 직전에 실행된다. **데이터 싱크를 맞추기 위해서 사용**

4. afterUpdate는 
state 값이 할당되어 돔이 변경된 직후에 실행된다. **데이터 싱크를 맞추기 위해서 사용**

```ts

let div;
let autoscroll;

beforeUpdate(() => {
	autoscroll = div && (div.offsetHeight + div.scrollTop) > (div.scrollHeight - 20);
});

afterUpdate(() => {
	if (autoscroll) div.scrollTo(0, div.scrollHeight);
});

```
-> 값이 바뀌기 전에 스크롤을 내려줘 챗봇이 답하는 내용을 바로 볼 수 있도록 도와주는 로직 


### 이벤트 Forwarding

1. 돔 이벤트와 다르게 components 이벤트는 버블되지 않는다. 만약 중첩된 컴포넌트의 이벤트를 감지해서 현재 위치의 요소가 변경되기를 원할땐 중간의 컴포넌트가 이벤트를 보내야한다고 한다. 
해결 방법 : Outer.svete에서  createEventDispatcher 사용하는 법 밖에 없다.
```ts
// app.svelte -> outer.svelte -> inner.svelte

//outer.svelte
<script>
	import Inner from './Inner.svelte';
	import { createEventDispatcher } from 'svelte';

	const dispatch = createEventDispatcher();

	function forward(event) {
		dispatch('message', event.detail);
	}
</script>

<Inner on:message={forward}/>

--> 스벨트는 이벤트를 포워딩하는데 유용한 코드 단축을 제공해준다.
//like this


<script>
	import Inner from './Inner.svelte';
</script>

<Inner on:message/>

```
메세지에 아무 인자도 넣지 않으면 createEventDispatcher을 만들고 포워드 함수 안에서 디스패치를 사용한 것과 같은 기능을 한다고 한다... 


```ts
// 상위 컴포넌트
<script>
	import CustomButton from './CustomButton.svelte';

	function handleClick() {
		alert('Button Clicked');
	}
</script>

<CustomButton on:click={handleClick}/>

// 하위 컴포넌트

<button on:click>
	Click me
</button>
```
alert이 나온다. 양방향 바인딩이 가능한 것 같다.

### action
액션은 tag, 엘리먼트 단위의 라이프 사이클 함수라고 한다. 
```ts
<form 
	action="/register/"
	use:enhance
>							
	label
	input
	button 
</form>
```

### context와 stores 뭐가 다른거지? 
stores는 어디에서나 사용 가능하나, 컨텍스트는 컴포넌트 혹은 하위 컴포넌트에서만 사용이 가능하다. 

1. stores : 전역 상태 관리. 단일 소스 상태를 유지하고 Store를 사용하면 상태를 변경하는데 필요한 모든 로직을 Store 내에 캡슐화할 수 있다. 오호!! 

2. context : 상위 컴포넌트에서 Context를 생성하고 하위 컴포넌트에서 해당 값을 사용할 수 있다. Context 값은 Provider 컴포넌트를 통해 설정하고 Consumer 컴포넌트를 통해 접근 가능

따라서 Context는 부모와 하위 컴포넌트 사이에서 값을 공유하기 위한 방법이고, Store는 전역 상태를 유지하고 상태 변경에 대한 로직을 캡슐화하는 방법이다.

### Question 
1. svelte에서는 onClick 시 fetch 혹은 axios를 활용해서 서버와 통신을 하는데 svelteKit에서는 use:enhance와 같은 것을 사용하던데... 이 부분이 아직 햇갈린다. 혹시 아시는지 여쭤보고 싶었습니다. 




# 차이
## 리액트와의 차이 
1. [[virtual-dom]]을 사용하지 않는다. 
-> 그렇다면 변경된 상태를 어떻게 효율적으로 업데이트하는거지? 
-> 컴파일러가 더욱 최적화된 JS코드를 만들어서 빠르게 UI를 업데이트할 수 있도록 한다. 
2. 메모리 차이
-> 리액트는 diffing algorithm이 무거워서 그런지 30 ~ 110 MB이지만 svelte는 15~30MB다. 실로 놀랍다. 



## 나만의 언어로 정리



### 출처(참고문헌)

### 연결문서
- [[react MOC]]
- [[svelteKit]]
- [[vue]]
- [[AngluarJs]]
