# React batches state updates
### You will learn

-   여러개의 state를 어떻게 업데이트 시키는지 [[batching]]이 뭔지
-   How to apply several updates to the same state variable in a row

## 리액트는 state update를 묶어서 실행한다.
```js
   <button onClick={() => {
        setNumber(number + 1);
        setNumber(number + 1);
        setNumber(number + 1);
      }}>+3</button>
```

원인 
1. 각 랜더의 state values are fixed.

2. (batching) 리액트는 state 업데이트 과정 전에 eventHandler의 모든 코드가 실행될 때 까지 기다린다. -> 상태 업데이트가 나중에 된다? -> setNumber() 다음에 리렌더 되는 이유이다. 


# Updating the same state variable multiple times before the next render 

함수 형 업데이트 방식 사용하면 된다 

# 값을 바꾼 후 업데이트 하면 ? 

``` Js
<button onClick={() => {  

setNumber(number + 5);  

setNumber(n => n + 1);  

}}>

```

1.  `setNumber(number + 5)`: `number` is `0`, so `setNumber(0 + 5)`. React adds _“replace with `5`”_ to its queue.
2.  `setNumber(n => n + 1)`: `n => n + 1` is an updater function. React adds _that function_ to its queue.

> React stores `6` as the final result and returns it from `useState`.

# 업데이터 함수 정리
-  **An updater function** (e.g. `n => n + 1`) gets added to the queue.
-  **Any other value** (e.g. number `5`) adds “replace with `5`” to the queue, ignoring what’s already queued.

eventHandler 코드 실행이 끝나면 리액트는 렌더링이 일어난다. 리렌더링 동안 react는 queue를 처리하고 Update function은 랜더링 중에 실행되고 있어서 순수해야 결과를 반환한다. 


# 정리 
- state 설정을 했어도 해당 랜더에는 반영이 되지 않고 다음 랜더에 적용되는 특징이 있다.
- 리액트는 상태 업데이트를 eventHandler의 코드가 종료되면 실행한다. 이것을 batching이라고 한다.
- 한번의 이벤트에 동일한 상태를 여러번 업데이트를 하기 위해서 setState의 인자에 콜백함수를 넣어서 updater 함수를 만들어 사용한다.


