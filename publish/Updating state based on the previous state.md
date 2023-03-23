```Js
function handleClick() {  

setAge(age + 1); // setAge(42 + 1)  

setAge(age + 1); // setAge(42 + 1)  

setAge(age + 1); // setAge(42 + 1)  

}

function handleClick() {  

setAge(a => a + 1); // setAge(42 => 43)  

setAge(a => a + 1); // setAge(43 => 44)  

setAge(a => a + 1); // setAge(44 => 45)  

}
```


업데이트 함수는 보류중인 상태가 되고 이 상태로 부터 다음 상태값이 계산된다. 

업데이트 함수는 queue에 담긴다. 그래서 다음 렌더링시 순차적으로 호출한다. 

[[Queueing a Series of State Updates]]
