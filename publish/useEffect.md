
Up : [[knowledge_MOCs]]

출처 :
저자 :
URL : 
인용 : 

# reference
리턴값은 undefined
주의 
1. useEffect는 훅이라 컨포넌트 최상위에서 호출해야한다. 
2. 외부 시스템(서버) 데이터를 동기화하려고 사용해야한다. 
[[functional Update]]

# sideEffect란? 
[[side effect in react]]

클래스
![[스크린샷 2023-01-06 오후 1.25.53.png]]

함수형 
component , componentDidupdate



차이
-> 클래스 : method가 새로 만들어지지않는다. 그래서 useCallback이 필요하지 않은 것. 
-> 함수형 : 리랜더링이 될때 마다 method가 새로 만들어진다.



# useEffect란

#한마디정리 컴포넌트가 렌더링 이후 어떤 이팩트를 수행할지 제어하는 Hook

useEffect에 전달된 함수는 화면에 ==렌더링이 완료된 후==에 수행하게 된다. 

어떤 값이 변경되었을때만 실행되게 할 수도 있다. 의존성 배열 

useEffect가 뭐야? 
외부 시스템과 동기화를 맞춰주기 위해

그럼 Effect가 뭐지? 
-> 

## 사용 방식
- 서버와 클라이언트의 다른 상태를 동기화 
-> 

## useLayoutEffect
[[critical rendering path]] 의 layout 이후 동기적으로 발생
즉 paint 단계 이전에 수행된다. ==렌더링 완료되기 전,== -> 타이밍, 예측 가능성이 떨어질 것 같다. 

## 의존성 배열 
Q. 상태 아니고 파생된 값 혹은 그냥 값을 넣었을떄? 
-> 변수는 안바뀐다. state는 계속 변경! 그래서 상태만 들어간다. 

Q. a,b가 의존성 배열에 들어가야하는데 [a] , [a,b,c] 만 들어갔을 경우
-> 

## useEffect안에서 함수를 사용하자
``` js
function ProductPage({ productId }) {
  const [product, setProduct] = useState(null);

  async function fetchProduct() {
    const response = await fetch('http://myapi/product/' + productId); // productId props 사용    const json = await response.json();
    setProduct(json);
  }

  useEffect(() => {
    fetchProduct();
  }, []); // 🔴 `fetchProduct`가`productId`를 사용하므로 잘못되었습니다  // ...
}
```

```Js
function ProductPage({ productId }) {
  const [product, setProduct] = useState(null);

  useEffect(() => {
    // 이 함수 컴포넌트를 effect 내부로 이동하면 사용하는 값을 명확하게 볼 수 있습니다.    async function fetchProduct() {      const response = await fetch('http://myapi/product/' + productId);      const json = await response.json();      setProduct(json);    }
    fetchProduct();
  }, [productId]); // ✅ 효과는 productId 만 사용하므로 유효합니다  // ...
}
```

### 뭐를 이동 시킬수 없는 경우 몇가지 옵션 제안
1. 해당 함수를 컴포넌트 외부로 이동
2. 렌더링하는 동안 호출해도 안전하다면, 대신 Effect 외부에서 호출하고 반한된 값에 따라 effect가 달라지도록 할 수 있다. 
3. 마지막 수단 useCallback 



# 2.14 공유할 내용
useEffect 무한 렌더링 예시 
```js
// app.js
<div className="App">
	<div>{JSON.stringify(data)}</div>
	<div>
		<button onClick={() => setUrl("juyoung.json")}>ju</button>
		<button onClick={() => setUrl("sally.json")}>sa</button>
	</div>
	</div>
);

//useFetch.js
export const useFetch = (option) => {
console.log(option) // {url : "juyoung.json"}
	const [data, setData] = useState(null);
	useEffect(() => {
		console.log("useFetch");
		if (option.url) {
		fetch(option.url)
		.then((res) => res.json())
		.then((json) => setData(json));
		}
}, [option]); // option을 넣으면 무한 렌더링 


return {
	data,
	};
};


```

**핵심 : 의존성 배열** 
- useEffect , useCallback, useMemo의 의존성 배열 이해하기 

-> 원시값이 () 불리언, 숫자, 문자열은 **값**으로 비교되고 평가되는 것)이 의존성 배열에 있으면 다루기 쉽다. 
-> 참조형 데이터 타입이 [ ] 안에 있으면 문제가 발 생 할 수 있다.

> 그렇다면 위의 예시는 왜 문제가 있는거지?  -> useFetch로 들어오는 ==값이 object여서==!! 그래서 무한 랜더링에 빠지는 것. 


그럼 어떻게 해결하지? 
#### 1. 객체를 변수에 할당해서 변수를 useFetch로 넘겨줌 -> 항상 동일한 값이 넘어가 trigger 되지 않는다.
```js
const myOption = {
	url: "/juyoung.json",
};
```
-> 문제 : useEffect가 실행되지 않는다. 왜냐하면 참조값이 계속 동일하기 때문에 


#### 2. useMemo 사용 
```js
const myOptions = useMemo(() => (), [url]);
```
url에 state가 변할때만 다른 값으로 인식하도록!! 
-> 하지만 useMemo 사용 비추. 다른 방식으로 더 쉽게 관리할 수 있다. 

#### 3. 의존성 배열 값 좁히기 (원시형 타입으로 )
```js
//useFetch.js
export const useFetch = (option) => {
	const [data, setData] = useState(null);
	useEffect(() => {
		console.log("useFetch");
		if (option.url) {
		fetch(option.url)
		.then((res) => res.json())
		.then((json) => setData(json));
		}
}, [option.url]); // option을 넣으면 객채 -> option.url은 원시형 타입 그래서 무한렌더링에서 빠져나올 수 있다. 
```


### 생각의 연결고리
분야 :

키워드 :

관련있는 메모 : [[usages of useEffect]]
