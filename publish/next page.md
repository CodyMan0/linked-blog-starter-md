공식 문서 정리 

# SG
## 1. Pre-rendering
Next.js는 매 페이지에서 pre-render를 해준다. 사전에 HTML을 만든다는 의미. 이로인해 더 빠른 성능과 SEO에 유리
HTML 페이지는 최소한으로 필요한 자바스크립트를 가지고 있고 브라우저에서 로드됐을때 그 코드가 돌고 모든 상호작용을 할 수 있는 코드로 만드는데 이것을 Hydration이라고 한다. 

## 두가지 방식
1. Static Generation :  빌드 타임에 HTML을 생성
2. Server-side-Rendering: 매 요청때마다 HTML을 생성

넥스트는 자유롭게 사용자에게 설정할 수 있도록 한다. 

성능을 위해서는 SG를 사용하도록 권장

SG 를 살펴보자
1. 외부 데이터에 의존한 페이지일 경우
```tsx
export default function Blog({ posts }) {
  return (
    <ul>
      {posts.map((post) => (
        <li>{post.title}</li>
      ))}
    </ul>
  )
}
```

같은 파일에 export async가 붙은 getStaticProps 함수가 있다. 이 함수는 빌드타임에 호출되고 pre-render시에 해당 페이지에 props로 넘길 수 있다!! 대박

```jsx
export default function Blog({ posts }) {
  // Render posts...
}

export async function getStaticProps() {
  const res = await fetch('https://.../posts')
  const posts = await res.json()

  return {
    props: {
      posts,
    },
  }
}
```


2.  **외부 데이터에 의존한 페이지 경로!!** 내가 필요한 것
Next.js는 동적 라우팅과 함께 페이지를 만들 수 있도록 한다. like this pages/posts/[id] 빌드 타임에 외부 데이터에 따라 id를 넣어줄 수가 있다.

동적 라우팅 페이지에서는 [[getStaticPaths]]를 제공해준다. 


## SG를 써야할때는 ? 
SG는 가급적으로 언제든 써야한다고 하는데 그 이유가 CDN에 의해서 제공되고 한번만 빌드되면 되기 때문이라고 한다. 
#Q CDN과 SG 캐싱 조금 이해가 안간다.

써야할 때
-   Marketing pages
-   Blog posts and portfolios
-   E-commerce product listings
-   Help and documentation


# Server-side-Rendering
HTML이 매 요청마다 만들어지는 것.
사용하기 위해서 [[getServerSideProps]] 라는 함수를 사용해야하고 매 요청때마다 호출된다.


```jsx
export default function Page({ data }) {
  // Render data...
}

// This gets called on every request
export async function getServerSideProps() {
  // Fetch data from external API
  const res = await fetch(`https://.../data`)
  const data = await res.json()

  // Pass data to the page via props
  return { props: { data } }
}
```

 `getServerSideProps`과 차이는 빌드타임이 아닌 매 요청때 데이터 패칭을 한다는 것
 



