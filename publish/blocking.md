
---
aliases: []
tags : 
---
Up : [[HOME 🌎]]

출처 :
저자 :
URL : 
인용 : 


# blocking이란
자신의 작업을 진행하다가 다른 주체의 작업이 시작되면 다른 작업이 끝날때까지 기다렸다가 자신의 작업을 시작하는 것.


setTimeout과 동일한 동작을 하는 함수를 만들었을때

```js
function sleep(func, delay) {

const delayUntil = Date.now() + delay;

  

while (Date.now() < delayUntil) func();

}

  

function foo() {

console.log("foo");

}

  

function bar() {

console.log("bar");

}

  

sleep(foo, 3 * 1000);

  

bar();
```
![[스크린샷 2022-12-31 오전 11.28.14.png]]

# 블로킹 한계 극복
비동기 콜백으로 싱글 스레드의 한계를 극복할 수 있다. 






### 생각의 연결고리
분야 :

키워드 :

관련있는 메모 : [[AJAX]],[[Non-blocking]]

