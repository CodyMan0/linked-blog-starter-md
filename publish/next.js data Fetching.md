데이터 패칭은 가능한 서버 컴포넌트에서 하는 것을 추천. 
1. 동일한 환경에서 데이터를 받고 랜더가 이루어짐. Client와 server간에 통신을 줄일 수 있다는 의미.
2. 지역에 따른 상이한 데이터 fetching 성능을 향상시킬 수 있다. 

-> 클라리언트에서 fetching은 react-query사용 


서버에서 react-query를 사용하여 pre-render 시키는 방법
```ts

export default async function PostsPage(){
	const queryClient = getQueryClient();
	await queryClient.prefetchQuery(['posts'], getPostsQueryFn);
	const dehydratedState = degydrate(queryClient);
	
	reuturn (
		<ReactQueryHydrate = state={dehydratedState}>
			Post
		</ReactQueryHydrate>
	)
}

```