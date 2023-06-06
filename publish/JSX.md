**JSX(JavaScript Syntax eXtension)** 란 리액트에서 사용하는 자바스크립트 확장 문법입니다. 기존에 바닐라 자바스크립트를 통해 기능을 구현할 때, HTML에서 markup(마크업)된 부분들을 확인하면서 직접 해당 DOM에 접근하고 Event Listener를 부착하는 등 HTML과 자바스크립트 로직은 서로 긴밀하게 연결되어 있습니다. 

JSX는 **HTML**과 **자바스크립트 로직**을 하나의 자바스크립트 파일 안에서 모두 처리하기 위해 확장한 문법

등장 배경 : html 태그에 js가 연결하는 것이 불편해서 고민하다가 나온 것이 JSX

JSX로 작성한 코드는 브라우저에서 동작하기 전에 [Babel](https://babeljs.io/)이라는 transcompiler를 통해 일반 자바스크립트 코드 형태로 변환됩니다.


## React.createElement(component, props, ...children)
예시
```js
ReactDOM.render(
<div id="msg">Hello World!</div>,
mountNode
);

ReactDOM.render(React.createElement('div',{id:'msg'},'Hello World!'),mountNode))
```

## JSX 규칙
[[JS_Syntax]]

