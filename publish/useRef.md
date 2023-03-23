---
aliases: [useRef]
tags : 
---

출처 : 벨로퍼트 기술 블로그
저자 :
URL : https://react.vlpt.us/basic/12-variable-with-useRef.html
인용 : 

## useRef 형태
```js
const refContainer = useRef(initialValue);
```

## 본질
.current 프로퍼티에 변경 가능한 값을 담고 있는 **상자**(변수)

## return result
자바스크립트 객체
-> 랜더링이 되면 객체가 변한다. 
useRef()는 매번 렌더링을 할때 ==동일한 ref객체==를 제공한다. 
-> 렌더링을 하더라도 객체가 변경되지 않는다. 


## useRef 사용법
1. 특정 DOM 을 선택할때 사용하는 용도 
2. 컴포넌트 안에서 ==조회 및 수정 할 수 있는 변수를 관리==


## useRef 특징 
- `useRef` 로 관리하는 변수는 값이 바뀐다고 해서 컴포넌트가 리렌더링되지 않습니다.
- `useRef` 로 관리하고 있는 변수는 설정 후 바로 조회 할 수 있습니다. state와의 차이
-> state는 setState 동작원리 스케줄러.
-> ref는 변경해도 렌더링이 되지 않고 객체니깐 값이 변경


이 변수를 사용하여 다음과 같은 값을 관리 할 수 있습니다.
1. `setTimeout`, `setInterval` 을 통해서 만들어진 `id`
2. 외부 라이브러리를 사용하여 생성된 인스턴스
3. scroll 위치


Ref는 render 메서드에서 생성된 DOM 노드나 React 엘리먼트에 접근하는 방법을 제공합니다.

# 라이프 사이클 관리 
-> useState, useEffect를 같이 설명하면 좋겠다. 
useRef! 



### 생각의 연결고리
분야 :

키워드 :

관련있는 메모 : 
