참고 :  https://ko.reactjs.org/docs/reconciliation.html

- 두가지 트리를 비교할때 시작점은 root element.

## 엘리먼트의 타입이 다른 경우
두 엘리먼트 타입이 다르면 React는 이전 트리를 버리고 완전히 새로운 트리를 구축한다.

## 엘리먼트의 타입이 동일한 경우
```tsx
<div className='before' title="stuff"/>
<div className='after' title="stuff"/>
```
이럴 경우는 className만 style도 마찬가지!! 여기서 잠깐 엘리먼트 타입이 중요한 역할을 하는구나? 


## 같은 타입의 컴포넌트 엘리먼트

## 자식에 대한 재귀적 처리
[[react presentation metarial]]

돔 노드의 자식을 가상돔에서 처리할 때 두 트리를 동시에 순회하고 차이가 있으면 변경을 생성한다. 여기서 
```jsx
<ul>
  <li>first</li>
  <li>second</li>
</ul>

<ul>
  <li>first</li>
  <li>second</li>
  <li>third</li>
</ul>
```
이럴 경우는 위에서 아래로 코드를 확인하는 알고리즘이 변한 부분만 확인해서 변경하면 효율적이나 

```jsx
<ul>
  <li>Duke</li>
  <li>Villanova</li>
</ul>

<ul>
  <li>Connecticut</li>
  <li>Duke</li>
  <li>Villanova</li>
</ul>
```
이런식으로 앞에 추가되면, 같은 선상에 있는 모든 노드들을 유지하는 대신 변경한다.

이러한 비효율적인 reconciliation을 막기 위해서 Keys가 있는 것. 


```jsx
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


key를 사용하지 않고 배열의 인덱스를 key로 사용할 수 있지만 항목들이 재배열되는 경우 비효율적으로 동작할 것입니다.