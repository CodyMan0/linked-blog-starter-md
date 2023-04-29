공식 문서 : https://kit.svelte.dev/docs/introduction
참고 문서 : https://heropy.blog/2019/09/29/svelte/
[[svelte working process]]

## 주제 : svelte
브라우저에 실행될떄 하는 모든 과정을 사이트가 배포 되기 전에 미리 다 해둔다. 하지만 생긴지 별로 안됐기 때문에 기능이나 커뮤니티가 덜 쌓인 부분들이 있다.

## Svelte란
리액트와 뷰와 다르게 프레임워크 혹은 라이브러리가 아니라 컴파일러에 가깝다. 스밸트가 JS 코드로 브라우저가 이해할 수 있도록 컴파일을 해준다. 그래서 프레임워크 혹은 라이브러리를 다운로드할 필요가 없다. 그렇게 되면 SPA인 Svelte는 소스코드를 브라우저가 렌더링을 할떄 HTML을 받아오고 CSS와 JS를 받아온다. 그때 JS가 타 라이브러리보다 가볍기에 빨리 로드되고 결과적으로 TTV(유저가 화면을 보는데 걸리는 시간)이 축소돼 SPA의 단점을 보완한게 아닐까 생각이 든다. 

## 사용 방법 
1. script : 상단에 script 태그 삽입시 자바스크립트 혹은 타입 스크립트를 사용할 수 있다.
2. style : style 태그 삽입시 css 스타일링이 가능하다.
3. HTML : 하단에 HTML 태그를 작성하면 끝. 


## 기본적으로 제공해주는 svelte 기능 
1. 유저 인풋과 값을 DOM에 더욱 쉽게 연결

```js
<script>
let name = '';
</script>

<input bind:value={name}>
<h2>hello {name}</h2>
```


## 강의에서 나온 스벨트 개념들 정리 

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


### 통신 설정
1. 실제 서버와 통신하는 여러 함수의 공통적인 부분을 service / api.js에서 모듈화 하여 사용하고 있으며 그 모듈을 사용하기 위해 해당 모듈 아래에서 함수를 만들어 참조하고 있다. 다른 컴포넌트에서 get,post,put,delete를 서버에 요청하고 싶을때 모듈을 사용하는 것이 아닌 모듈을 참조하고 있는 함수를 사용하면 되도록 설계하심. 


### 마크업으로 비동신 처리 

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
이미 만들어진 스토어를 기반으로 새로운 리턴값을 만드는 스토어, 불변하다는 특징을 가지고 있다.  또한 비동기저으로 작동한다.
```js
const storeName = derived(a , $a => {
	retrun $a + 1
})
```

### 스토어
#### writable 함수의 내장 매소드
1. subscribe(구독)
2. set
3.  update


#### 값 사용 함수
1. get : 다른 스토어에서도 값을 참조하는 경우에 사용되거나 일반 자바스크립트 파일에서 store 값을 가지고 올떄는 무조건 get 
2. set : 
3. update : 

#### 스토어 사용 기준
1. 변화된 부분만 반영하여 불필요한 데이터 호출을 막기 위할때 (update)


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


### props 사용 
1. 자식이 Props를 사용하기 위해선.
```js
export let props
```

2. 데이터를 수정할떄, props를 그대로 받아서 view에 뿌려주지 않고 객체에 프로퍼티에 재선언을 해줘 값을 불변하게 만들어줘! 수정하다 취소를 눌렀을때 수정한 값이 반영되지 않도록 진행한다. 





### 궁금한 것.
1. svelte에서는 onClick 시 axios를 활용해서 서버와 통신을 하는데 svelteKit에서는 use:enhance와 같은 것을 사용하는데 좀 햇갈린다.

2. 중복을 방지하기 위해 알려주신 코드
```js
	const uniqueArr = newArticles.filter(
		 (arr, index, callback) => index === callback.findIndex((t) => t.id === arr.id)
		);
	datas.articleList = uniqueArr;
```
혹시 어떻게 이해하셨는지? 



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
- [[vue]]
- [[AngluarJs]]
