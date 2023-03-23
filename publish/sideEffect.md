

 특히, ==프로그램을 이루는 가장 작은 단위인 함수==에서 쓰이는 용어입니다. 프로그래밍에서 함수가 하고자 하는 본질적인 역할은 무엇일까요? 
 
 함수의 ==주된 목적==은 **Input을 받아서 output을 산출하는 것**입니다. 
 
 따라서, 함수의 `부작용` 이란 **함수의 목적인 Input을 받아서 output을 산출하는 것 이외의 모든 행위** 
 
 [[pure function]] 이외의 모든 것을 sideEffect라고 하는건가??
 
### 클로저도 사이드 이펙트다

```js
const num = 1;
const sum = (x) => {   
	return x + num; };
```

위 예시에서 `sum` 함수는 `x`라는 `input`을 받아서 `x + num` 을 `return` 하고 있습니다. 이 함수는 side effect를 가지고 있습니다. 함수 내부의 값이 아닌 외부의 값인 `num`을 읽어오고 있기 때문입니다. 


첫번째) 함수가 함수 내부의 값(local state)를 제외한 나머지 값(non local state)들을 읽어올 때 side effect가 있다고 표현할 수 있습니다.

[[클로저 기본]]과 연관 그렇다면 클로져에서 다른 스코프의 변수를 읽을때도 sideEffect가 일어났다고 볼 수 있다. 
  

### 콘솔과 DOM 조작도 사이드 이펙트다
DOM을 조작하고, console에 특정 문자를 출력하는 행위 또한 함수 외부에 존재하는 DOM과 console의 상태를 변경시키는 것이기에 side effect


## 사이트 이펙트는
1.  **외부의 값을 읽어오는 행위**
2.  **외부의 값을 변경하는 행위**를 의미합니다.

그렇다면, 프로그래밍에서 side effect는 기피해야 하는 대상일까요?  
yes
  ->  **왜냐하면 side effect가 있는 함수는 동작 결과를 예측하기 쉽지 않기 때문입니다.** 유지보수를 어렵게 한다. 
  
따라서, 개발자들은 side effect를 최소화 하면서 프로그램을 설계하되, side effect가 필요한 경우에는 그것을 반드시 통제 가능하게 만들어서 side effect가 프로그램의 유지보수에 악영향을 주지 않도록 주의를 기울여야 합니다.


[[side effect in react]]
# 2. React에서의 Side Effect

---

## 2-1. 함수 컴포넌트에서의 input과 output

[[Rendering in react]]이 뭐야? 





  
 