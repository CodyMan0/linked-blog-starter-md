---
aliases: []
tags : 
---
Up : [[HOME 🌎]]

출처 :
저자 :
URL : 
인용 : 


var은 선언되면 window 객체의 키로 생긴다.

![[스크린샷 2022-11-21 오후 2.42.44.png|500]]

이렇게 되면 **단점은** 뭐가 있을까? 
let , const 는 scope에 저장되는데  var는 window 객체 안에 생성된다.

- 내 생각
1. 불필요한 [[scope chaining]]을 막을 수 있다? 
	왜? scope에 있다면 여기서 자바스크립트가 처리하면 끝인데 없다면 global까지 가야하니깐? 
2. global은 복잡한 공간이지 않나? 이름도 겹치면 안되니 최대한 global scope에에 변수를 선언하지 않는게 좋지 않을까? 



자바스크립트 변수 찾는 순서 : local -> script -> global(window)





정리 
1. 식별자로 변수를 선언하지 않으면 그냥 global scope의 키로 들어간다. 
2. 글로벌 컨텍스트에서 실행한 var는 global scope인 window로 들어갔는데 함수 안에서 실행하면 local로 값이 들어간다.  


### 생각의 연결고리
분야 :   

키워드 : [[호이스팅]]

관련있는 메모 : [[call stack]]


