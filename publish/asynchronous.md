
Up : [[knowledge_MOCs]]

## 핵심
한번 비동기는 영원한 비동기
비동기는 순서의 문제

## 동기
그 작업이 끝나길 "**기다렸다가**" 다음일을 진행한다.
값이 필요할떄는 동기식이어야한다. 


## 비동기 (순서의 문제)
그 작업이 끝나길 "**안 기다리고**" 다음일을 진행한다. 
수행과 관련없을때 비동기를 사용 

특징 
1. 비동기 처리 결과를 외부에 반환이 안되고
2. 상위 스코프의 변수에 할당이 안된다. 

그래서 비동기 함수의 처리 결과에 대한 후속 처리는 미동기 함수 내부 에서 수행해야한다. 
비동기는 값을 어떻게 받아오지? 

-> [[callBack]]으로 들어오게 해준다.
-> callBack 지옥으로부터 [[Promise (js)]] 더 나악 [[async-await]]이 등장

## 차이 
동기는 함수의 실행 후 값이 리턴될때까지 기다리고 다음 함수를 호출하는 반면, 비동기는 함수가 실행하고 종료하기 전에 바로 다음 함수를 실행하는 것을 말한다. 

## 한계 
1. 에러 처리의 한계 



### 생각의 연결고리
분야 :

키워드 :

관련있는 메모 : [[event loop]], [[blocking]] , [[Non-blocking]], [[async_principle]]
