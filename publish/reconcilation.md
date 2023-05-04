# 재조정 과정

리액트는 가상돔을 업데이트 하며 화면을 그려낸다. 

화면 업데이트는 **렌더 단계(render phase)**, **커밋 단계(commit phase)**로 나눠진다. 

전자는 실제 돔에 반영할 변경 사항을 파악하는 단계이고, 커밋은 파악된 변경 사항을 실제 돔에 반영하는 단계다.

[[react render and commit]]



### Key

key를 정해주어야 할때는 보통 배열의 요소를 mapping해줄 때 사용한다. 이때 key를 전달하지 않으면 리액트는 error를 던진다. 그 이유는 같은 tag가 반복되는 상황에서 순서만을 이용하게 되면 DOM요소가 변경되었을 때 전체를 다 변경해야하는 불필요한 비용이 발생하기 때문이다.


```
// DOM
<ul>
  <li>Duke</li>
  <li>Villanova</li>
</ul>

// VDOM
<ul>
  <li>Connecticut</li>
  <li>Duke</li>
  <li>Villanova</li>0
</ul>
```

위 코드와 같은 경우 react는 순서만으로 비교해 모든 요소가 다 바뀌었다고 이해하고 전체를 다 새롭게 DOM요소를 만든다. 이점을 해결하기 위해서 key를 이용한다면 내부 순서와는 상관없이 key값이 바뀐 요소만 찾아서 DOM을 업데이트해 최적화가 가능하다. 그렇기 때문에 **고유한 값**으로 key를 정해주는 것이 중요하며 key로 index를 직접 넘기면 안된다는 것이 이해가 되었다.

```
<ul>
  <li key="2015">Duke</li>
  <li key="2016">Villanova</li>
</ul>

<ul>
  <li key="2014">Connecticut</li>
  <li key="2015">Duke</li>
  <li key="2016">Villanova</li>
</ul>
```

