루트 : [[react MOC]]

## 1. 단일 엘리먼트를 리턴한다.
```ts
<div>  
	<h1>Hedy Lamarr's Todos</h1>  
	<img  src="https://i.imgur.com/yXOvdOSs.jpg"  alt="Hedy Lamarr"  
	class="photo"  
> 	 
	<ul>  
	...  
	</ul>  
</div>
```
동일한 계층에 여러 element가 있을때는 fragment 혹은 div를 활용하여 하나의 루트 노드를 만들어 컴포넌트의 리턴으로 넘긴다. 

Q. 왜 감싸야하는거지? 
JSX는 HTML 같은데 실제로는 JS 객체로 변환된다. 그래서 배열로 감싸지 않는 이상 하나의 함수로부터 두개의 객체가 반환되지 못한다. 


40장 : [[Event]]
스코프 : [[scope]]
스프레드 연산자 : [[Spread operator syntax]]