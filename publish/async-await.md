---
aliases: []
tags : 
---
Up : [[HOME 🌎]]

출처 :
저자 :
URL : 
인용 : 

# async/await 도입 배경
[[제너레이터]]와 [[Promise (js)]]를 사용해서 비동기 처리를 동기 처리처럼 동작하도록 구현했던 과거... 
하지만 보기에 장황하다는 단점이 있었다. 
그래서 ES8에서 가독성 좋게 비동기 처리를 **동기 처럼 동작하도록 구현할 수 있는 async/await**이 도입

## async 키워드 
함수 앞에 async를 붙히면 해당 함수는 promise 객체 함수로 변환된다. 

## await 키워드 
프로미스가 settled 상태가 될때까지 대기하다가 settled 상태가 되면 프로미스가 resolve한 처리 결과를 반환한다

## 에러 처리 
비동기 처리를 위한 [[callBack]]의 단점 중 심각한 것 -> **에러 처리**, 
콜백함수는 try catch문을 사용해 에러를 캐치할 수 없다.
async/await은 try...catch문을 사용할 수 있다. 


# 한마디 정리 
1. Generator는 중간에 실행을 중단하고 원하는 시점에 재개할 수 있는 특별한 함수
2. Generator 객체는 자체 실행 컨텍스트를 가지고 있다.  우선 오키! 
3. Generator and Promise를 통해 비동기를 동기적인 코드처럼 처리가능
4. 현재는 Async/Await 패턴으로 표준화됐다.  

# 모르는 것
1. async, await이 왜 try,catch가 되는지? 
-> try ,catch 쓰고 
2. 콜벡 패턴이 try,catch가 왜 안되는지? 
-> setTimeout 때문에 에러를 처리할 컨텍스트가 없으니깐, 
3. it is not iterable 에러를 많이 봤는데 
-> 원인 : iterable 객체가 없으니깐!!Symbol.iterator이 없으니깐 안되는 거였다 .





#면접문제 1,2(실행컨텍스트의 문제)



### 생각의 연결고리
분야 :

키워드 :

관련있는 메모 : [[제너레이터]] , [[Promise (js)]]
