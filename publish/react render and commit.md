[공식문서](https://react.dev/learn/render-and-commit#step-2-react-renders-your-components)

화면에 컴포넌트가 표현되기 전, 컴포넌트는 리액트에 의해서 랜더가 일어난다. 


trigger :  props 혹은 상위 혹은 자신의 state의 변화
rendering. : 그 모든 변화들을 처리하기 전 행위
commit : 모든 변화들의 최종본을 DOM을 반영하는 행위 

# 주제 
- 리액트에서의 랜더링이란?
- 언제? 왜? 리액트가 컴포넌트를 렌더시키는지
	when
	- 컴포넌트가 mount되면 initial render
	- 상위 컴포넌트 혹은 자신의 state가 변경(setState)되면 
- 화면에 컴포넌트를 보여지기까지의 단계들
	- rendering
	- commit : 
		- 첫 렌더 : appendChild() DOM API를 활용하여 스크린에 구현
		- 리 렌더 : diffing을 통해 최종 마지막 업데이트가 동기화된 내용을 DOM에 반영
- 왜 매 랜더링마다 DOM을 업데이트하지 않는지? 
- 브라우저 렌더링과 리렌더링
	- 리액트 랜더링 단계가 끝나면 커밋 단계가 이루어진다. 브라우저는 리페인트를 한다.


