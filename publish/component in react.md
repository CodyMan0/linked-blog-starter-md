
---
aliases: []
tags : 
---
Up : [[knowledge_MOCs]]

출처 : https://react.dev/learn/your-first-component
저자 :
URL : 
인용 : 

정의 : 컴포넌트란  html을 넣을 수 있는 js 함수이다.

```js
export default function Profile() {
  return (
    <img
      src="https://i.imgur.com/MK3eW3Am.jpg"
      alt="Katherine Johnson"
    />
  )
}

```

### Step 1: 컴포넌트 export 하기  

하단에 `export default`를 활용하여 컴포넌트를 다른 컴포넌트에서도 사용할 수 있도록 한다.

### Step 2 컴포넌트( 함수)의 return 
1. 한 줄이면 
```js
return <img src="https://i.imgur.com/MK3eW3As.jpg" alt="Katherine Johnson" /> 
```
2. 여러 줄일때 
```js
return (  
<div>  
	<img src="https://i.imgur.com/MK3eW3As.jpg" alt="Katherine Johnson" />  
</div>  
);
```



##  중첩하여 컴포넌트 사용하기 
컴포넌트는 자바스크립트 함수이기에 한 파일에서 여러개의 컴포넌트를 사용할 수 있다. 
### 생각의 연결고리
분야 :

키워드 :

관련있는 메모 :
