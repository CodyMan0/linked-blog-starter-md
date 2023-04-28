

## 동작 원리 
참고 : https://itchallenger.tistory.com/892

1. styled-components는 css를 lazy하게 생성하고 삽입한다.
-> 컴포넌트 렌더링 전까지 탬플릿 리터럴의 css 규칙을 cssom에 반영하지 않는다. 렌더링이 이루어지는 컴포넌트에 대해서만 css를 반영한다. 
2. styled-components는 css 규칙을 추가한다. 
-> document.stylesheets[0],styleSheet.insertRule(rulesets)

styled-components를 사용하면 JS 코드로 작성되고 이말인 즉슨 런타임 중에 실행된다는 것이다. 그래서 cssom 트리에 반영되지 않고 페이지가 로드되는 동안 동적으로 생성된다. 
styled-components는 SSR을 통해 스타일을 사전에 렌더링한다고 한다. 서버에서 JS 코드에서 정의된 스타일에 따라 css 규칙을 생성한다. 

중요한 것은 런타임에 css 규칙이 생성된다는 것!! 


### 내부 원리

```jsx
const red = '빨간색';
const blue = '파란색';

function favoriteColors(texts, ...values) {
   return texts.reduce((result, text, i) => 
   `${result}${text}${values[i] ? `<b>${values[i]}</b>` : ''}`, '');
}

favoriteColors`제가 좋아하는 색은 ${red}과 ${blue}입니다.`

// 제가 좋아하는 색은 <b>빨간색</b>과 <b>파란색</b>입니다.
```

styled-componenet는 런타임에 스타일이 씌어진다



### 생각의 연결고리
분야 : [[runtime]]

키워드 :

관련있는 메모 :


