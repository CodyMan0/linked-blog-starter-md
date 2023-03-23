
Up : [[knowledge_MOCs]]

출처 : 블로그 
URL :https://hsp0418.tistory.com/171
인용 : 

1. 리액트에서 불변성을 지켜야하는 이유 : [[useState]]을 활용하여 상태를 업데이트하는 원리때문

2. 리액트의 [[virtual-dom]]은 상태값을 업데이트할때 [[얕은 비교]]를 통해 수행
-> 즉 배열이나 객체의 속성을 비교하는게 아니라 이전 참조값과 현재 참조값만을 비교해서 상태 변화를 감지한다. 

그래서 setState에서 [[Spread operator syntax]]를 사용해서 업데이트를 해준거구나! 
```js
// 원시타입
const [number, setNumber] = useState(0) setState(3) // 참조타입
const [person, setPerson] = useState({ name: '', age: 30 }) setState({...person, name: 'ju-young'})

```


### 생각의 연결고리
분야 : [[functional Update]]

키워드 :

관련있는 메모 :
