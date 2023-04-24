
출처 : 
저자 : 


# 강의
1. react-queyr key 설정하는 방식
- /posts -> ["posts"]
- /posts/1 -> ["posts", id]
- /posts?authorId =1 -> ["posts", {authorId : a}]
- /posts/2/comments -> ["posts" , post.id, "comments"]


2. 리액트 쿼리의 refetch 특성 
- 리액트 쿼리는 stale하다고 판단한 데이터를 refetch하는 특징이 있다. 이를 해결하기 위해
```js
const queryClient = new QueryClient({
defaultOptions: { queries: { staleTime: 1000 * 60 * 5 } },
});
```
최상위에 stale 해지는 시간을 정해주면 동일한 쿼리 키가 호출될때 위의 지정한 5분은 refetch되지 않고 계속 fresh 상태를 지속할 수 있다. 그말인 즉슨 불필요한 fetch를 막는다는 것. 

3. preFetch도 할 수 있다.
```js
	function onHoverPostOneLink() {
		queryClient.prefetchQuery({
			queryKey: ["posts", 1],
			queryFn: () => getPost(1),
		});
	}

	<button
		onMouseEnter={onHoverPostOneLink}
		onClick={() => setCurrentPage(<Post id={1} />)}
	>
		First Post
	</button>
```

4. 의존성이 있는 쿼리 만들기
```js
  const postQuery = useQuery({
    queryKey: ["posts", id],
    queryFn: () => getPost(id),
  })

  const userQuery = useQuery({
    queryKey: ["users", postQuery?.data?.userId],
    enabled: postQuery?.data?.userId != null,
    queryFn: () => getUser(postQuery.data.userId),
  })
```

enabled 프로퍼티에 불리언 값을 사용하여 postQuery의 data의 userid가 null(비어있다)이 아닐때 요청한 쿼리에 대한 응답을 받아올 수 있다. 만약 없다면 3번정도 refetch가 일어난 후, 에러 상태를 받는다. 

5. useMutation에서 
```js
	queryClient.setQueryData(["posts", data.id], data);
	queryClient.invalidateQueries(["posts"], { exact: true });
```
invalidateQueries와 setQueryData 정리 
- invalidateQueries를 활용하여 동일한 쿼리키를 무효화할 수 있다. 변수나 하위키가 없는 posts 쿼리만 무효화하려는 경우에는 exact : true 옵션을 사용할 수 있다. 
- setQueryData는 


# 카카오 페이 프론트 react-query 
React Query는 React Application에서 서버의 상태를 불러오고, 캐싱하며, **지속적으로 동기화**하고 업데이트 하는 작업을 도와주는 라이브러리입니다.

# 블로그 

`react-query`는 서버의 값을 클라이언트에 가져오거나, 캐싱, 값 업데이트, 에러핸들링 등 비동기 과정을 더욱 편하게 하는데 사용됩니다.


# 0. 유데미 강의
## client State

단순히 사용자의 상태를 추적
## Server state 
블로그 게시물의 데이터 
fetch나 axios를 사용하지 않고 react query 캐시 요청을 한다. 

## 역할
1. 데이터 패칭
2. 로딩과 에러처리를 수동으로 하지 않아도 된다
3. pagination/ infinite scroll
4. prefetching
5. Mutation
6. De-duplication of requests
7. Retry on error



# 1 . 우아한 테크 세미나 강의 

## FE 상태 관리에 대해서 
==정리:== 프로덕트의 규모가 커지면서 상태도 복잡혀진다. 그래서 상태를 체계적으로  관리해야하는 필요성이 생기기 시작했다.
Q. 프론트에서 상태관리는 어떤 것을 하는 건가요? 
내 생각) 웹사이트의 서버간에 가지고 있는 값을 관리하는 것?  (특정할 수 없다.)
발표자 ) 라이브러리가 먼저 떠오른다. (redux, mobx, recoil)
-> 상태란 관리해야하는 데이터들

#### 배경 
UI/UX의 중요성과 함께 프로덕트 규모가 커지면서 관리하는 ==상태==가 많아진다.  -> 상태관리의 필요성 증가 


## reactQuery와 상태관리 
store에서 전역상태를 관리해야하는데 점점 API코드만 쌓였다? 내가 생각한것과 비슷하다 . -> 이 말인 즉은 상태관리 영역이 서버 값을 저장하는데까지 확장했다고 한ㄷ. 이게 궁금했는데

관리하고 싶은 상태들의 특성을 파악하라


![[스크린샷 2022-09-25 오전 10.35.23.png|500]]
key point : ownership이 어디있는지에 따라 달라진다.

global state 터치하는 아무것도 없이 리액트 내에서 fetch cache 그리고 데이터를 업데이트! 
==정리==
서버에서 데이터를 가져오고 캐시해주고 동기화 그리고 데이터 업데이트를 해주는 라이브러리


![[스크린샷 2022-09-27 오전 8.08.05.png|500]]
1. 캐쉬를 관리할 키값
2. 어디에 API를 패칭해서 가져올 Promise함수가 들어간다.
3.


### useQuery Funtion

 ![[스크린샷 2022-09-27 오전 8.09.07.png|500]]
 
-> 공식문서에 너무 잘 나와있다. 

### useQuery Option

![[스크린샷 2022-09-27 오전 8.16.04.png|600]]
-> config는? 어디에 설정?
-> enabled: false로 하면 mount되는 시점에 실행을 시키지않을 수 있다. 

-> calling 기능 만들때 refetchInterval 사용하면 알아서 구현해준다.

## React Query Mutations
데이터 생성 , 수정 , 석제 


## React Query Mutation option
![[스크린샷 2022-09-27 오전 8.41.21.png|500]]


QueryClient.invalidateQueries() 불러오면 끝. 이렇게 하면
해당 Key를 가진 query는 state취그비 되고 현재 rendering이 되고 있는 query들은 백그라운드에서 Refetch된다.


## React query 캐싱과 동기화
- RFC 5861
-> http Cache-Control extensions for stale content ^449d3a

[[stale-while-revalidate]]가 존재하면 api를 찌르는

```cache-control : max-age=600, stale-while-revalidate=30```

#비유 새물건 오기 전에 옛날 물건 보여준다?

- cacheTime: 메모리에 얼마만큼 있을건지(해당시간 이후 GC에 의해 처리,default 5분) 
- staleTime: 얼마의 시간이 흐른 후에 데이터를 stale 취급 할 것인지 (default 0 )

### query 상태 흐름

![[스크린샷 2022-10-06 오전 9.33.02.png]]

### zero-config
1. staleTime -> 0
2. refetchOnMount/refetchOnWindowFocus/refetchOnReconnect -< true
3. cacheTime -> 60 * 5 * 1000 5분
4. retry-> default 값 3번



-> 리액트 쿼리 선언적이라 사용자도 잘 몰랐지만 캐싱부분을 해결 할 수 있다. 
[[caching]] 내 언어로 정리해보기 


 




### 생각의 연결고리

분야 :

키워드 :

관련있는 메모 : [[Optimistic Update]], 
