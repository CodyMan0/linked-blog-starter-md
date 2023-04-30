
![](https://velog.velcdn.com/images/sharphand1/post/2a68758c-c373-4781-bfc8-c024f218fc96/image.png)



## Svelte란 ❓
react 그리고 vue와 다르게 프레임워크 혹은 라이브러리가 아니라 컴파일러에 가깝습니다. svelte는 JS 코드로 브라우저가 이해할 수 있도록 컴파일을 해줍니다. 프레임워크 혹은 라이브러리를 다운로드할 필요가 없다는 것. 리액트나 뷰는 브라우저에서 해당 소스 코드를 다운로드 받아야합니다. 그렇게 되면 다소 무겁지 않을까요? SPA(single page application)인 Svelte도 유저가 접속하면 해당 HTML을 받아오고 CSS와 JS를 받아옵니다. 그때 JS가 타 라이브러리보다 가볍기 때문에 빨리 로드되고 결과적으로 TTV(유저가 화면을 보는데 걸리는 시간)이 축소돼, SPA의 단점을 보완한게 아닐까 생각이 듭니다. 리액트, 뷰, 앵귤러, 스밸트 모두 HTML이 하나여서 SPA라고 합니다. 


## 리액트와 뷰와 차이
리액트와 뷰는 우리로 하여금 선언적인 코드를 작성할 수 있도록 도와줬으나 많은 패널티가 있었습니다. Dom에 변경 사항을 반영하기 위해 추가적인 작업(diffing)을 요구 했던것. 그로 인해 비용과 GC(메모리 누수 방지 기능)에게 부과적인 일이 요구됐다. 대신 스벨트는 빌드 타임(베포를 하기 전, 번들해주는 단계)에 운영됩니다. 그래서 선언적으로 작성한 컴포넌트를 효과적으로 명령형 코드로 변환해준다. 그 결과 엄청난 성능의 어플을 만들 수 있게 됐다. 

스벨트는 컴파일러이기 때문에 뒷단에서 우리가 모르는 일을 해준다.
```ts
//스테이트를 만들면 
count += 1 

//컴파일러는 코드를 이렇게 해석한다
count += 1; $$invalidate('count', count)

```


## Virtual DOM 복습하기 
리액트는 render() 함수안에서 JSX 문법으로 작성되고 props or State 가 바뀌었을때 reconcile이 일어납니다. 가상돔 때문에 성능이 빠르다는 것은 거짓부렁까지는 아니지만 확실한 것은 사실은 아니다라는 것... 그래서 svelte는 가상돔 자체를 쓰지 않는 방법을 채택했다고 합니다. 


## Svelte 태그 사용법 
1. script : 상단에 script 태그 삽입시 자바스크립트 혹은 타입 스크립트를 사용할 수 있다.
2. style : style 태그 삽입시 css 스타일링이 가능하다.
3. HTML : 하단에 HTML 태그를 작성하면 끝. 

```ts
<script>
  let count = 1
  let emailValue = ''
  funtion submitHandler ...
</script>

<form on:submit={submitHandler} id = 'user_form'>
    <label>email</label>
	<input on:input bind:value={emailValue}>인풋</input>
</form>

<style>
  #user_form {
    background-color : red;
	...
	}
</style>
```



## ⌛ 강의에서 나온 스벨트 개념 정리 

### state (상태를 의미)
스벨트에서 state(DOM 업데이트를 trigger하는 값)를 만들기가 간편하다.
```ts
let count = 0 
//리액트보다 간편하다. 그저 변수에 값을 할당만 해주면 된다.
```

### props 사용 
1. 자식 컴포넌트가 Props(스테이트를 자식으로 내리면 그 값을 Props라 지칭)를 사용하기 위해선 자식 컴포넌트에 아래 코드를 작성하면 됩니다. 
```js
export let answer;
```

2. 받은 Props의 값을 default로 설정하기 위해선.
```ts
// 부모.svelte
// 부모에서 Children을 import해서 사용하고 있다는 것은 부모 컴포넌트 
// 하위에 자식 컴포넌트가 있다는 것. 
<script>
  import Children from './Children.svelte'
</script>

<Children>
  

// 자식.svelte
<script>
	export let answer = 'a mystery';
</script>

	<p>The answer is {answer}</p> 
// 상위 컴포넌트에서 state를 넘기지 않으면 Default 값이 들어간다.
// <p>The answer is {answer}</p> : The answer is 'a mystery'
</script>
```

3. 객체인 스테이트를 props로 내려줄때는 spread 연산자를 사용할 수 있다.

```ts
<script>
	import Info from './Info.svelte';

	const svelte = {
		name: 'svelte',
		version: 3,
		speed: 'lightening',
		website: 'https://svelte.dev'
	};
</script>

<Info name={svelte.name} version={svelte.version} speed={svelte.speed} website={svelte.website}/>
  
// 위와 같이 일일이 내려줄 수 있지만 state가 객체 일땐 아래와 같이 보낼수도 있다. 
<Info {...svelte}/> 
```



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


### 강의 아키텍처
1. 실제 서버와 통신하는 여러 함수의 공통적인 부분을 service / api.js에서 모듈화 하여 사용하고 있으며 그 모듈을 사용하기 위해 해당 모듈 아래에서 함수를 만들어 참조하고 있다. 다른 컴포넌트에서 get,post,put,delete를 서버에 요청하고 싶을때 모듈을 사용하는 것이 아닌 모듈을 참조하고 있는 함수를 사용하면 되도록 설계하심. 


### 마크업으로 비동신 처리 
> 예시) 공식문서 

```ts
{#await promise}
	<p>...waiting</p>
{:then number}
	<p>The number is {number}</p>
{:catch error}
	<p style="color: red">{error.message}</p>
{/await}
```

> 예시) 인프런 강의

간단한 설명 : auth.refresh() 함수는 JWT(유저를 식별하고 권한을 부여하는 일련의 토큰 방식)를 활용하여 두개의 토큰을 부여하는데 그 중 하나인 refresh token이 유효한지를 확인하는 함수입니다. 추상화가 잘 되어있어 auth.refresh() 함수를 사용하면 기능을 사용할 수 있습니다.

최상위 컴포넌트에서 auth.refresh()를 사용해도 되고 
```js
// main.js
await auth.refresh(); // 여기서 await을 해서 호출해도 정상작동하기는 함
```

최상위 바로 밑 컴포넌트에서 마크업을 활용해서 auth.refresh()로 판단할 수 있습니다.
```js
//App.svelte
<div class="main-container">
  {#await auth.refresh() then}
    <Router />  
  {/await}
</div>
```

-> 둘다 정상 작동합니다.
auth 스토어에서 refresh 함수의 결과값이 True 일때 그때서야 Router 컴포넌트를 실행시키겠다는 의미입니다. 즉 refresh 토큰에 의해서만 라우터가 이동될 수 있게 만드는 것. 인증이 된 유저에게 페이지로 이동할 권한을 주는 것입니다.


### 스토어
#### 1. writable store
읽기, 쓰기가 가능한 스토어로 Set과 Update 메서드를 지원한다. Set은 값을 초기화하는 메서드이고, Update는 값을 수정하는 메서드입니다. Update의 경우 파라미터로 콜백 함수가 전달되는데, 콜백 함수의 파라미터로 스토어의 현재 값이 전달됩니다. 콜백 함수를 리턴하면 스토어의 값이 수정됩니다.

```ts
// Store.js
import { writable } from 'svelte/store'

export const exampleStore = writable(초기값)


// 사용할 컴포넌트.svelte
<script>
  import { exampleStore } from 'Store.js 경로'

  function setStoreFunc () {
    exampleStore.set(초기화 값)
  }

  function updateStoreFunc () {
    exampleStore.update((현재 스토어 값) => {
      return 업데이트할 값
    })
  }
</script>
```
살짝 어렵죠...?

#### 2. Unsubscribe / Auto Subscribe
메모리 누수를 막기 위해 구독을 중지하는 방식으로 사용되는데 우선 넘어가겠습니다!!

#### 3. Readable Store
Svelte에서 스토어 사용 시 대부분은 읽기 / 쓰기가 가능한 Writable 스토어를 사용하지만, 경우에 따라서 값을 바꿀 수 없고 참조만 가능한 스토어를 사용해야할 수 있습니다. 예를 들어, 브라우저의 마우스 위치나 브라우저의 스크린 크기 등 외부에서 변경하는 것이 의미 없는 데이터가 필요한 경우가 있을 것이다. 이 경우 Readable 스토어를 사용하여 읽기 전용 데이터를 표현할 수 있다.

```ts
import { readable } from 'svelte/store.js'

export const exampleStore = readable(초기값, function (setFunc) {
  // 스토어 값 설정 시 실행되는 작업

  setFunc(스토어에 설정할 값)

  return function initStoreFunc(){
    // 스토어 초기화 시 실행되는 작업
  }
})
```

#### 4. Derived store

이미 만들어진 스토어를 기반으로 새로운 리턴값을 만드는 스토어, 불변하다는 특징을 가지고 있다.  또한 **비동기적**으로 작동합니다. 비동기적이라는 것은 일종의 100M 달리기를 비유로 생각하면 쉽습니다. 동일한 선상에서 동시에 출발한다고 생각하면 됩니다. 즉 순서에 상관없이 각자 자신이 해야할 것들을 하는것 입니다. 

```js
//app.svelte
<script>
	import { time, elapsed } from './stores.js';

	const formatter = new Intl.DateTimeFormat('en', {
		hour12: true,
		hour: 'numeric',
		minute: '2-digit',
		second: '2-digit'
	});
</script>

<h1>The time is {formatter.format($time)}</h1>

<p>
	This page has been open for
	{$elapsed} {$elapsed === 1 ? 'second' : 'seconds'}
</p>


//store.js
import { readable, derived } from 'svelte/store';

export const time = readable(new Date(), function start(set) {
	const interval = setInterval(() => {
		set(new Date());
	}, 1000);

	return function stop() {
		clearInterval(interval);
	};
});

const start = new Date();

// derived 함수로 기존 store 값이 time을 변경합니다.
export const elapsed = derived(
	time,
	$time => Math.round(($time - start) / 1000)
);
```


#### 5. Store Binding
쓰기가 가능한 스토어의 경우 (Writable 스토어, 사용자 정의 스토어 중 set 메서드가 있는 경우) 컴포넌트에서 양방향 바인딩 기능을 사용할 수 있다. 리액트는 단방향 바인딩을 할 수 있습니다. (부모에서 자식에게만 데이터를 보내느 것을 의미) 하지만 스벨트는 약간 다르다고 생각됩니다. 




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
fetch는 onMount 함수 안에서 사용하는 것을 권장한다고 합니다. 

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
-> 값이 바뀌기 전에 스크롤을 내려줘 챗봇이 답하는 내용을 바로 볼 수 있도록 도와주는 로직입니다. 


### 이벤트 Forwarding

1. 돔 이벤트와 다르게 components 이벤트는 버블되지 않는다. 만약 중첩된 컴포넌트의 이벤트를 감지해서 현재 위치의 요소가 변경되기를 원할땐 중간의 컴포넌트가 이벤트를 보내야한다고 합니다.

해결 방법 : Outer.svete에서  createEventDispatcher 사용하는 법 밖에 없습니다. 아래 코드를 살펴보면

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


## 리액트와의 차이 
1. virtual-dom을 사용하지 않는다. 
-> 그렇다면 변경된 상태를 어떻게 효율적으로 업데이트하는거지? 
-> 컴파일러가 더욱 최적화된 JS코드를 만들어서 빠르게 UI를 업데이트할 수 있도록 한다. 
2. 메모리 차이
-> 리액트는 diffing algorithm 연산 비용이 커서 그런지 30 ~ 110 MB이지만 svelte는 15~30MB다. 실로 놀랍다. 





### 출처(참고문헌)
1. [나의 옵시디언 메모](https://www.juyoungdev.com/svelte)
2. 공식 문서 : https://kit.svelte.dev/docs/introduction
3. 참고 문서 : https://heropy.blog/2019/09/29/svelte/