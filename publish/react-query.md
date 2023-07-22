# 7.11 공식 문서를 통해 재정리 
출처 : https://tanstack.com/query/v3/docs/react/overview
https://github.com/ssi02014/react-query-tutorial

## 개요 
리액트 쿼리는 서버 상태를 loading, fetching, cacheing, synchronizing, updating이 가능하게 한다. 

## 배경
웹 프레임워크에서는 데이터를 가져오고 업데이트는 방식을 제안하지 않아 현재 상태 관리 라이브러리를 사용하여 앱 전체에 걸쳐 비동기적으로 데이터를 관리하고 있다. 

대부분의 상태 관리 라이브러리는 클라이언트 상태에는 적합하고 잘 동작하지만 비동기와 서버상태에는 그리 훌륭하지는 않다. 왜냐하면 서버 상태는 전혀 다르기 때문. 그럼 서버 상태가 무엇인지에 대해 알아야한다.

서버 상태는
1. 제어할 수 없는 위치에 원격으로 보관돼야한다.
2. 비동기 APIs를 활용하여 데이터를 가지고오고 업데이트 해야한다.
3. 조심히 다뤄야한다 왜냐하면 상태가 구식(stale)이 될 수 있기 때문에

서버 상태에 대한 이해가 생기면 여러가지 어려움을 마주하게 된다.

1. 캐싱, 프로그래밍에서 생각보다 어려운 주제
2. 같은 데이터를 여러번 요청 제어
3. 뒷단에서 stale 데이터 업데이팅
4. stale한 데이터를 인지하는 것
5. 최대한 빠르게 업데이트한 데이터를 반영하는 것
6. 페이지네이션이나 레이지 로딩 데이터 성능 최적화 
7. 서버 상태의 GC와 메모리 관리

위의 문제들을 리액트 쿼리는 해결하고 있다. 리액트 쿼리 공식문서에서는 자칭 서버 상태를 다르는데 최적화된 라이브러리는 자신이라고 한다.  


## 바로 시작하기!! 
리액트 쿼리를 제대로 알기 위해서는 3개의 구성 요소로 이루어졌다는 것을 알아야한다.

### 1. Queries
#### Query 기본 
쿼리는 비동기 데이터와 묶여있는 유니크 키의 의존성이라고 한다. 즉 쿼리를 통해 비동기 데이터를 가지고 올 수 있다는 의미이다. useEffect의 의존성 배열에 id state가 있다면 id state가 변경될 경우 해당 useEffect가 실행된다는 의미에서 동일하다고 생각한다. 

쿼리는 Promise 객체로 사용되고 만약 테이터를 변경할 경우에는 Mutations를 사용하는 것을 추천한다. 

그럼 조금 더 자세히 알아보자 


로직을 분리하기 위한 커스텀 훅 혹은 컴포넌트에서 쿼리를 구독하기 위해선 useQuery라는 훅을 선언하면 되는데 조건이 있다.

1. query 키는 유일해야한다.
2. Promise 객체를 반환하는 함수는 데이터를 Resolves 하거나 에러를 던져야 한다는 것. 


예를 들면 

```tsx
import { useQuery } from '@tanstack/react-query'
function App() { 
	const info = useQuery({ queryKey: ['todos'], queryFn: fetchTodoList })
}
```

위에 보이는 쿼리 키는 내부적으로 어플리케이션 전역에 다른 쿼리와 공유되기에 꼭 유일해야한다. 
유일한 쿼리에 해당하는 값은 useQuery가 포함하고 있는 쿼리에 대한 모든 정보에 의해서 반환된다.

결과 객체는 몇가지의 중요한 상태를 포함한다. 순간 마다 상태가 달라지기에 정확히 알아야 효율적으로 사용할 수 있다고 한다. 
1. isLoading 은 그 쿼리에 데이터가 아직 없는 상태
2. isError는 그 쿼리를 통해 데이터를 불러오려다 에러를 만난 상태
3. isSuccess는 데이터를 사용할 수 있고 성공적으로 가지고 온 상태

위의 세개의 중요한 상태 이외에 두가지가 있다. 
1. error는 만약 쿼리가 isError 상태일때 error 프로퍼리를 통해서 에러 값을 사용할 수 있게 해준다.
2. data는 isSuccess 상태일때 값을 사용할 수 있게 해준다.

#### FetchStatus
status 필드 외에도 결과 객체에는 추가적인 프로퍼티인 fetchStatus를 확인할 수 있는데 다음과 같다.
1. fetchStatus === fetching 는 쿼리가 fetching하고 있다는 것을 의미한다.
2. fetchStatus === paused 는 쿼리가 fetching하려 하지만 잠시 멈춰있다는 의미이다.
3. fetchStatus === idle 는 그 순간에 어떤 것도 하지 않는다는 의미이다.

#### 왜 두 상태가 있는거지? 
뒷단에서는 refetches와 오래된 데이터를 판단하는 로직이 위에서 살펴본 status와 fetchStatus 프로프티를 통해 결과 객체에 담기는 것을 가능하게 한다. 예를 들면

1. success인 쿼리는 보통 idle fetchStatus이지만 동시에 fetching 상태일 수 있다. 뒷단에서 refetching을 할 경우가 있을 수 있다.
2. 브라우저에 마운트한 동시에 데이터가 없는 상태인 쿼리는 lodaing 이면서 fetching 상태일 수 있다. 만약 네트워크가 연결되지 않았다면 동시에 paused 상태가 될 수 있다는 것을 말한다.
여기서 명심해야하는 것은 쿼리는 데이터를 fetching 하고 있지 않으면 loading 상태라는 것. 

정리하면 
status는 데이터에 대한 정보를 제공하고 
fetchStatus는 queryFn에 대한 정보를 제공한다.


### 2. Mutations
위에서 살펴본 쿼리와 다르게 전형적으로 서버 데이터를 CRUD 혹은 서버 상태로 인한 사이드 이펙트를 발생시킬때 사용한다. 목적에 맞게 Tanstack query에서는 useMutation 훅을 제공해준다. 

간단한 공식 문서 예시 코드를 살펴보면 

```tsx
function App() {
  const mutation = useMutation({
    mutationFn: (newTodo) => {
      return axios.post('/todos', newTodo)
    },
  })

  return (
    <div>
      {mutation.isLoading ? (
        'Adding todo...'
      ) : (
        <>
          {mutation.isError ? (
            <div>An error occurred: {mutation.error.message}</div>
          ) : null}

          {mutation.isSuccess ? <div>Todo added!</div> : null}

          <button
            onClick={() => {
              mutation.mutate({ id: new Date(), title: 'Do Laundry' })
            }}
          >
            Create Todo
          </button>
        </>
      )}
    </div>
  )
}

```

여기서도 mutation의 상태를 살펴보면
1. isIdle은 mutation이 현재 idle하다는 것 
2. isLoading은 현재 진행하고 있다는 것
3. isError은 에러를 만난 것
4. isSuccess는 변경된 데이터를 사용할 수 있고 성공적으로 끝났다는 것

query와 마찬가지로 위의 상태를 값으로 사용하려면 error와 data가 있다. 개념은 동일하다. 

위의 코드에서 mutation.mutate() 함수를 살펴보면 그 안에 원시형 변수 혹은 객체가 들어가야 호출된다고 한다. 

Mutation은 onSuccess 옵션과 함께 사용되거나 Query Client의 invalidateQueries 메서드와 setQueryData 메서드와 함께 사용할때 제대로 사용할 수 있다고 한다. 

#### mutate 리셋으로 돌리기
```tsx
const CreateTodo = () => {
  const [title, setTitle] = useState('')
  const mutation = useMutation({ mutationFn: createTodo })

  const onCreateTodo = (e) => {
    e.preventDefault()
    mutation.mutate({ title })
  }

  return (
    <form onSubmit={onCreateTodo}>
      {mutation.error && (
        <h5 onClick={() => mutation.reset()}>{mutation.error}</h5>
      )}
      <input
        type="text"
        value={title}
        onChange={(e) => setTitle(e.target.value)}
      />
      <br />
      <button type="submit">Create Todo</button>
    </form>
  )
}
```

#### 서버 값을 변경하여 사이드 이펙트 (훅) 일으키기 
useMutation은 옵션이 있는데 그 옵션은 변경되는 라이프 사이클 동안 사이드 이팩트를 빠르고 쉽게 일으켜 준다. 이 옵션으로 인해 서버 상태가 변경되고 유효하지 않은지 판단하고 다시 데이터를 패칭하는데 있어서 유용하다. 

```tsx

useMutation({
  mutationFn: addTodo,
  onMutate: (variables) => {
    // A mutation is about to happen!

    // Optionally return a context containing data to use when for example rolling back
    return { id: 1 }
  },
  onError: (error, variables, context) => {
    // An error happened!
    console.log(`rolling back optimistic update with id ${context.id}`)
  },
  onSuccess: (data, variables, context) => {
    // Boom baby!
  },
  onSettled: (data, error, variables, context) => {
    // Error or success... doesn't matter!
  },
})
```

mutationFn , onMutate , onError, onSuccessm onSettled

#### retry
tanstack query에서는 자동적으로 mutation 과정에서 에러를 만나면 retry가 되지 않지만 옵션을 통해 제어할 수 있다.

```tsx
const mutation = useMutation({
  mutationFn: addTodo,
  retry: 3,
})
```



### 3. Query Invalidation
쿼리가 다시 fetching 전에는 오래된 상태가 되기를 기다리는 기능이 기본적으로 작동하는 것은 아니다.  stale한 데이터가 되면 refetching해주도록 하기 위해서는 QueryClient의 invalidateQueries() 매소드를  사용해야한다. 

invalideQueries 안의 쿼리가 오래 되면 두가지가 발생한다.

1. stale이라고 표기된다. 관련된 훅 혹은 useQuery 안에서 사용되는 staleTime 구성을 오바라이딩한다.
2. 만약 그 쿼리가 useQuery 혹은 관련 훅을 통해 최근 랜더링 되면 뒷단에서 refetching된다. 

#### invalidateQuereis와 연결한 쿼리 

invalidateQueries와 removeQueries와 같은 API를 사용할 때 (그리고 부분 쿼리 일치를 지원하는 다른 API들), 접두사를 사용하여 여러 쿼리를 일치시킬 수도 있고, 정확한 쿼리를 사용할 수 있다.

예를 들어 공식문서에 나와있는 코드를 보면
```tsx

import { useQuery, useQueryClient } from '@tanstack/react-query'

// Get QueryClient from the context
const queryClient = useQueryClient()

queryClient.invalidateQueries({ queryKey: ['todos'] })

// Both queries below will be invalidated
const todoListQuery = useQuery({
  queryKey: ['todos'],
  queryFn: fetchTodoList,
})
const todoListQuery = useQuery({
  queryKey: ['todos', { page: 1 }],
  queryFn: fetchTodoList,
})
```

queryClient.invalidateQueries() 안에 'todo' 라는 쿼리키가 있는데 아래의 두 useQuery 모두 쿼리를 매칭한 것이다.
또한 특정 쿼리 변수와 함께 매칭할 수도 있다고 한다. 

invalidateQueries APIs는 유연한데 만약 todo 쿼리키만 있고 하위 변수 혹은 하위키가 없는 쿼리만 무효화하고 싶으면 exact 속성을 true로 설정하면 된다. 

```tsx

queryClient.invalidateQueries({
  queryKey: ['todos'],
  exact: true,
})

// The query below will be invalidated
const todoListQuery = useQuery({
  queryKey: ['todos'],
  queryFn: fetchTodoList,
})

// However, the following query below will NOT be invalidated
const todoListQuery = useQuery({
  queryKey: ['todos', { type: 'done' }],
  queryFn: fetchTodoList,
})
```



# 2.11 정리 
React Query는 React 애플리케이션에서 데이터 관리를 간편하게 해주는 JavaScript 라이브러리이다. 서버로부터 데이터를 가져오고, 캐싱하고, 상태 관리하며, API와의 상호 작용을 처리하는 데 도움을 준다 React Query는 서버로의 데이터 요청을 처리하기 위해 Promise 기반의 API를 제공하며, 이를 사용하여 비동기 데이터를 관리할 수 있습니다.

## 주요 개념

1.  Query: 서버로부터 데이터를 가져오는 요청을 나타냅니다. React Query는 데이터를 가져오고 캐시하며, 필요한 경우 데이터를 다시 가져올 수 있다.
    
2.  Mutation: 서버에 데이터를 수정하는 요청을 나타냅니다. React Query는 상태 업데이트 및 캐시 갱신과 함께 비동기 작업을 처리합니다.
    
3.  캐싱: React Query는 서버로부터 가져온 데이터를 자동으로 캐싱합니다. 이를 통해 빠른 데이터 접근과 성능 향상을 이끌어냅니다.
    
4.  상태 관리: React Query는 데이터의 로딩 상태, 에러 상태, 데이터 유효성 검사 등과 같은 다양한 상태를 추적합니다. 이를 통해 UI를 업데이트하고, 로딩 상태에 따른 UI 변화를 쉽게 처리할 수 있습니다.
    
5.  조건부 요청: React Query는 요청을 조건부로 만들 수 있습니다. 예를 들어, 데이터가 캐시에 없는 경우에만 서버로 요청을 보내도록 설정할 수 있습니다.
    
6.  자동 재요청: 네트워크 연결이 불안정하거나, 데이터가 만료된 경우, React Query는 자동으로 재요청을 시도합니다. 이를 통해 사용자 경험을 향상시킬 수 있습니다.
    

React Query는 React 컴포넌트와 원활하게 통합되며, React의 상태 관리 기능과 함께 사용할 수 있습니다. 또한, 다양한 플러그인과 함께 사용하여 더욱 강력한 기능을 추가할 수 있습니다.

React Query는 개발자에게 데이터 관리 작업을 단순화하고, 반복적인 코드를 줄여주며, 성능을 향상시키는 데 도움을 줍니다


