## 사전 지식 
- [[event loop]]를 알고 있어야하는 것 같다.
- [[kinds of event loop]]
- [[Implementation of setTimeout and setInterval scheduling functions ]]
- [[클로저 기본]],[[클로저 다지기]]
- 
- 


debounce and throttle

debouncing timer가 0.5초라는 것은 0.5초 미만일 경우에는 이벤트가 발생해도 clearTimeout을 통해 초기화시켜주고 0.5초가 지나서야 eventListener 실행하주는 것을 말한다. 

throttle은 0.5초라는 시간안에서 수많은 이벤트중 eventListener이 한번 실행하다는 의미!! 



하고자 하는 것 
![[스크린샷 2022-11-11 오후 3.54.54.png||300]]
이 코드를 정확히 이해하는 것을 목표로 한다. 