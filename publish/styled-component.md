
---
aliases: []
tags : 
---
Up : [[HOME 🌎]]

출처 :
저자 :
URL : 
인용 : 


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


