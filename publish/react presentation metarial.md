
# 리액트 가상돔

## 사전 학습
Q. [[critical rendering path]] 알고 있는지 확인해봅시다. 


## 리액트 등장 이유
**문제 상황** :  **MPA** -> SPA 

**해결** : 리액트는 **이전 UI 상태를 in-memory에 유지하는 가상 DOM**을 통해 변경될 UI의 최소 집합을 계산하여 DOM 처리 횟수를 최소화하고 효율적으로 진행합니다.


### SPA가 생긴 배경을 이해하고 보는 가상돔
웹페이지에서 조그마한 부분이 변경되는 경우에도 전체다 새로고침이 이루어졌던 과거의 웹페이지.  사용자 경험의 관점에서 볼때는 좋지 않았습니다.  그래서  간결한 문법으로 DOM을 편리하게 다룰 수 있고 크로스 브라우징을 용이하게 해준 jQuery 가 몇년 전까지만 해도 인기가 좋았지만 크로스 브라우징의 필요성이 줄어들고 순수한 자바스크립트도 발전을 했기때문에 Jquery가 힘을 잃게 됐다. 


가상돔은 DOM의 구조만 간결히 흉내낸 **자바스크립트 객체**, 시뮬레이션([[diffing algorithm]])을 돌려 가장 경제적으로 돔에 변화를 가하는 방식을 찾아낸 것.  ==가상돔을 조작할떄 마다 layout , paint 과정을 거치지 않는다.== 

가상돔 사용 --> [[react MOC]] , [[vue]] (라이브러리 혹은 프레임 워크)
가상돔 사용하지 않음 --> [[svelte]] 

[[가상돔의 비교 원리]]

가상돔은 용도 : 브라우저단에서 효율적으로 무엇을? 해내기 위해 만들어졌다.

## 가상돔 동작 과정 
###  재조정 (reconciliation)

```jsx
 const element = (
  <>
   <h3>React:</h3>
   <form>
    <input type="text" />
   </form>
   <span>Time: {new Date().toLocaleTimeString()}</span>
  </>
 );
 console.log(element)
```

위의 코드가 아래처럼 변환되는데 아래 코드가 가상돔이다. 가상돔은 userInterface를 나타낸다. 

![[스크린샷 2022-12-20 오전 9.12.46.png]]


위의 과정을 **재조정(Reconcilation)** 이라고 부른다.
랜더링이 이뤄지면 리액트는 UI를 나타내는 가상돔 객체를 만들고 메모리에 가지고 있습니다.
그리고 랜더가 이루어지면 새로운 가상돔을 생성하여 값을 비교해서 바뀐 부분만 자동으로 업데이트를 해주는 방식

Q. 그런데 재조정은 어떻게 이루어지는가?  이전 값을 [[diffing algorithm]]을 사용해서 가지고 있는 다음 무슨 변화가 필요한지를 찾는게 **reconciliation*

비교하고 업데이트가 되는 과정 이후에 리액는 리액트돔이라는 라이브러리가 사용됩니다. rendered app을 업데이트 하기 위한 정보를 가지고 옵니다. 이 라이브러리는 실제 돔이 repaint된 가상돔을 받을 수있도록 합니다. 


![[스크린샷 2022-12-20 오전 9.25.30.png]]


actual dom에서는 바뀐 데이터만 repaint가 됩니다. 

예시

![[화면 기록 2022-12-20 오전 9.26.41.mov]]

### 재조정은 diff 알고리즘으로 되는거한데...
React Fiber라는 재조정 엔진으로 인해서 reconciliation이 이루어지는 것이었다. 








### 관련있는 메모
[[Functional programming]],

## 리액트 useMemo와 useCallback
[[useMemo]]
[[useCallback]]
## 리액트 key를 사용해야하는 이유
비효율적인 reconciliation을 막기 위해서 Keys가 있는 것. 
[[react MOC]]
## 참고자료


virtual dom : https://blog.logrocket.com/virtual-dom-react/#virtual-dom-object

immutability : https://blog.logrocket.com/immutability-react-should-you-mutate-objects/

key : https://betterprogramming.pub/why-react-keys-matter-an-introduction-136b7447cefc

## 추천 블로그
https://velog.io/@superlipbalm/blogged-answers-a-mostly-complete-guide-to-react-rendering-behavior