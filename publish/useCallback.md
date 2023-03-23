---
aliases: []
tags : 
---

출처 :
저자 :
URL : 
인용 : 

## 나의 생각
useMemo 는 특정 **결과값을 재사용** 할 때 사용하는 반면, useCallback 은 **특정 함수를 새로 만들지 않고 재사용하고 싶을때** 사용합니다. 정리해보면 useCallback은 리랜더링으로 인한 함수의 재설정으로 인한 sideEffect를 방지하는 훅이라고 생각?! 

## 근간
useCallback은 useMemo를 기반으로 만들어졌다. 

```Jsx
const onToggle = useMemo(
  () => () => {
    /* ... */
  },
  [users]
);
```

### 주의 
 함수 안에서 사용하는 상태 혹은 props 가 있다면 꼭, `deps` 배열안에 ==포함==시켜야 된다는 것 입니다. 
 만약에 `deps` 배열 안에 함수에서 사용하는 값을 넣지 않게 된다면, 함수 내에서 해당 값들을 참조할때 가장 최신 값을 참조 할 것이라고 보장 할 수 없습니다. props 로 받아온 함수가 있다면, 이 또한 `deps` 에 넣어야한다.


```jsx
 const onToggle = useCallback(
    id => {
      setUsers(
        users.map(user =>
          user.id === id ? { ...user, active: !user.active } : user
        )
      );
    },
    [users]
  );
```

##  효과
렌더링시 render phase는 실행이 되지만 함수가 새로 만들어지는 것을 방지함으로써 props를 동일하게 해주었으므로  commit phase는 실행되지 않는다.  

❓ 그럼 랜더 phase까지 막을 수 있는 방법이 있나?
[[React.memo]]를 활용하면 된다


### 생각의 연결고리
분야 :

키워드 :

관련있는 메모 : [[useMemo]]
