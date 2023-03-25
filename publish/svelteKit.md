---
aliases: []
tags : 
---
Up : [[knowledge_MOCs]]

출처 :
저자 :
URL : 
1. 공식 문서 : https://kit.svelte.dev/
2. 유튜브 
	1. simon Grimm : https://www.youtube.com/watch?v=RKiMX58bLvI
인용 : 



## 캐치 프레이즈
1. 성능
2. 재미 : 번들러 라우팅, 환경 설정이 간편
3. 유연성 : 모든 방식의 Application을 만들 수 있다. 

핵심 
svelte는 file System Routing이 이루어지고 있다.
자동적으로 서버에서 랜더된다.





## 투두리스트 with svelteKit
[[투두리스트]]



## 튜토리얼 
스벨트킷은 빌드시에 최적화된 자바스크립트 코드로 변환시킨다. 런타임에 실행시키지 않는다. 프레임워크로 인한 성능 저하를 겪을일이 없다는 의미. 

- 컴포넌트 파일의 확장자는 .svelte
- 상태를 리얼돔과 동기화하는 시스템이 스벨트킷의 강력한 시스템
- 스벨트의 반응성은 리얼돔과 동기화를 시켜줄뿐 아니라 반응형 선언을 사용하여 변수를 서로 동기화
- 반응형 선언은 할당에 의해 트리거가 된다. 배열과 객체의 메소드를 통해서 요소들이 바뀐다고 해서 트리거가 되지 않음
```js
	$: sum = numbers.reduce((t, n) => t + n, 0); // 트리거가 되지 않음
	function addNumber() {
		numbers.push(numbers.length + 1);
	}
	$: sum = numbers.reduce((t, n) => t + n, 0); // 트리거됨. 
	function addNumber() {
	numbers = [...numbers, numbers.length + 1];
	}

```
- 컴포넌트 상단에 script 태그 안에 있는 변수는 해당 컴포넌트에서만 접근가능  export 붙혀줄 경우 상위 컴포넌트에서 props로 넣어서 사용할 수 있게 해준다. 
- 스벨트는 html 태크를 조건적으로 렌더할 수 있다. {#if}{/if}
```js
//if and else
{#if user.loggedIn}
	<button on:click={toggle}>
		Log out
	</button>
{:else}
	<button on:click={toggle}>
		Log in
	</button>
{/if}

//if and elseif and else
{#if x > 10}
	<p>{x} is greater than 10</p>
{:else if 5 > x}
	<p>{x} is less than 5</p>
{:else}
	<p>{x} is between 5 and 10</p>
{/if}
```
- react의 map과 같은 기능 데이터에 따라 UI 보여주는 법
```js
{#each cats as cat, i }
	<li><a target="_blank" href="https://www.youtube.com/watch?v={cat.id}" rel="noreferrer">
		{i + 1}: {cat.name}
	</a></li>
{/each}
//as뒤에는 .map((*) => ) * 와 같은 역할을 한다. 요소와 index를 표현 


{#each things as thing (thing.id)}
	<Thing name={thing.name}/>
{/each}
//스벨트에서도 key를 사용해야 정확히 삽입,삭제시 리얼돔이 무엇을 업데이트해야하는지 알려주는 것. 리액트와 비슷
 
```

- 비동기 로직을 html로 Promise를 다루는 법
```js

{#await promise}
	<p>...waiting</p>
{:then number}
	<p>The number is {number}</p>
{:catch error}
	<p style="color: red">{error.message}</p>
{/await}
 
```

- 컴포넌트 이벤트 (dispatch 사용 가능 )


### 기능
1. 반응형 선언 : 상태로부터 파생되는 값 (상태와 동기화되어있는 변수)
```js
$: doubled = count * 2; // 상태와 동기화된 변수

$: console.log('the count is ' + count); // 상태에 따라 콘솔을 찍어주는 변수 

$: if (count >= 10) {
	alert('count is dangerously high!');
	count = 9;
} // 상태에 조건을 줄 수 도 있다. 
```


### 생각의 연결고리
분야 :

키워드 :

관련있는 메모 :
