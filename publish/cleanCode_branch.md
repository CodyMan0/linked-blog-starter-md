1. 값식문 -> [[statement and expression]]
- [[react MOC]]는 [[JSX]]를 사용한다. 이 과정에서 많은 실수를 한다. 
- [[a higher-order function]] (고차 함수): map, filter, reduce
	-> JSX {} 안에는 값과 식만 들어가야한다. 

2. [[ternary operator]]
-> 조건이 복잡할떄는 switch case로 바꾸자 
-> Nullable한 값을 처리할떄 상항 연산자 처리 가능 

3. [[Truthy and Falsy]]

4. [[short circuiting trick]]

5. else if 피하기, else 피하기 
-> 논리적으로 반전된 로직을 작성하게 되어 기능을 망칠 수 있다. 
-> [[early return]]

6. 부정조건문 지양하기 #투두리팩토링
-> **생각을 더 해야한다**. 그래서 햇갈리게 됨. 읽기 어려운 코드가 되어버린다. 
-> if 문의 전제조건인 true를 뒤집으면 햇갈리게 됨. 
-> 부정 조건문 사용할때 [[early return]] 혹은 [[form validation]] 혹은 보안하고 검사하는 로직에 사용할 수 있다. 

7.  Default Case 고려하기 
```js
function sum(x,y) {
x = x || 1;
y = y || 1;

return x + y;
}

sum(100,200)
```
-> 사용자의 입력을 받는 프론트앤드단에서는 에러처리를 해주도록 노력해야한다. 
-> 사용자의 **실수를 예방**하자

8. 명시적인 연산자 사용 지양
-> ()를 사용을 적극 장려
-> 예측 가능한 코드를 만들어야한다. 

9. [[Null merge operator]]
->

10. [[De Morgan's Law]]







# 오늘 배운 것
falsy 값으로 값이 undefined일 경우 값을 할당






