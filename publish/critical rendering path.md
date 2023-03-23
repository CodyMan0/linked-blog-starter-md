
What is critical rendering path? 
크롬을 누르면 브라우저가 해당 url을 서버에 요청하고 필요한 정보를 서버가 응답으로 보내줬을 때,  html, css, javascript을 그려서 보여주는 과정인 critical rendering path을 살펴보면

CRP의 정의
`Critical Rendering Path(CRP)`는 브라우저가 서버로부터 HTML 응답을 받아 화면을 그리기 위해 실행하는 과정이다.


DOM 요소에 변화가 생기면 웹 브라우저는 다시 렌더 트리(DOM 트리 + CSSOM 트리)를 그리고, 레이아웃 위치를 계산하고(layout), 화면에 그리는 작업(paint)을 수행합니다. 

1.  HTML을 파싱해서 DOM을 만든다. 
2.  CSS를 파싱해서 CSSOM을 만든다.
3.  DOM과 CSSOM을 결합해서 Render Tree를 만든다.
4.  Render Tree와 Viewport의 width를 통해서 각 요소들의 위치와 크기를 계산한다.**(Layout)** -> [[flow, reflow ]]
5.  지금까지 계산된 정보를 이용해 Render Tree상의 요소들을 실제 Pixel로 그려낸다. **(Paint)**


+ 보강하기 

### 관련있는 메모

[[working process of browser]]