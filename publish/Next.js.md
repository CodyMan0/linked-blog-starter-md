
---
aliases: []
tags : 
---
Up : [[HOME 🌎]]

출처 :
저자 :
URL : https://www.youtube.com/watch?v=ECMB4kUCKWQ&t=448s
인용 : 
[공식문서](https://nextjs.org/learn/basics/create-nextjs-app)
https://www.reason-to-code.com/blog/why-we-couldn't-feel-the-difference-of-nextjs/
넥스트 작동방식 : https://velog.io/@surim014/how-next.js-works#%EA%B0%9C%EB%B0%9C-%EB%B0%8F-%ED%94%84%EB%A1%9C%EB%8D%95%EC%85%98-%ED%99%98%EA%B2%BD
App 라우터 작동 원리 : https://junghan92.medium.com/%EB%B2%88%EC%97%AD-next-js%EC%9D%98-app-%EB%94%94%EB%A0%89%ED%84%B0%EB%A6%AC-%EC%95%84%ED%82%A4%ED%85%8D%EC%B2%98-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-28672980d765
-> https://www.inngest.com/blog/5-lessons-learned-from-taking-next-js-app-router-to-production
# App router 사용 이유
## Why use the App Router?

1. loading을 없애기 위해 정적 렌더링(SSG)를 사용하여 즉시 보여준다.
2. spa에서의 새로고침이 없이 인증 리디렉션을 처리하는 미들웨어를 제공한다. 
3. 기본적으로 번들링과 code splitting을 제공
4. Edge 함수 도입을 도와준다.

### APP 라우터의 장점
1. 중첩 레이웃을 통해서 상태를 보존하고 비용이 많이 드는 렌더링을 해결할 수 있다. 
2. 서버를 더 사용하기 위해 React Server Components를 사용
3. streaming을 통해 모든 데이터를 로드하기를 기다리지 않고 페이지 일부를 빨리 표시할 수 있다. 
## 1. 두가지의 캐시 이해하기 
### 1. 클라이언트 캐시 
클라이언트 캐시는 라우트(url)에 사전에 가지고온 payload에 저장하여 네비게이션이 빠르게 느껴지도록하는 것

### 2. 서버 캐시
서버에서의 캐시란 서버 측 데이터를 가지고오는 성능을 향상시키는게 핵심

## 특징
1. layout component는 리렌더가 발생하지 않는다. 



# 공식문서 1독
-> SSR로 동작하는 어플이 브라우저에 어떻게 렌더링이 되는지 이해하기 위해 한번 읽는 것 

##  NEXT.js가 해결한 문제
1. 리액트와 같이 소스 코드는 웹팩과 같은 번들러와 바벨과 같은 컴파일러를 사용하여 변환해야했다. 
2. 베포시 최적화를 위해 코드 스플릿팅을 고려해야했다.
3. SEO를 위해 고정적으로 pre-render을 할 수도 있어야했고 SSR 혹은 CSR을 자유자재로 해야했다. 
4. React App의 한 곳에서 server-side code를 작성하고 싶었다. 

next.js는 위의 4가지를 해결했다. 

## 기본 문법
### CSR Navigation and code-splitting and prefetching
1. Link는 client-side navigation 할 수 있는 기능 
-> Client-side navigation이란 JS에 의해 발생되는 페이지 전환이라는 뜻, 일반적인 브라우저에 의해 일어나는 페이지 전환보다 빠르다는 특징이 있다. 
2. code splitting 그리고 pre-fetching
-> next.js에서는 코드 스플릿을 자동적으로 해준다. 각 페이지에서 로드에 필요한 최소한의 js만 로드하고 다른 페이지에 관련된 js는 로드 하지 않는다! 
-> 이 말인 즉슨 페이지가 현재 독립적이라는 것. 그래서 에러를 처리하는데도 용이하다. 
-> 베포된 프로덕션에서 LINK 컴포넌트가 보이면 next.js가 자동으로 연결된 페이지를 위해 pre-fetching을 해준다고 한다. 그래서 사용자가 LInk 컴포넌트를 클릭할땐 이미 뒷단에 로드가 완료된 상태이고 그 즉시 페이지가 변환되어진다는 것!! 

### Assets, Metadata, and css
1. Asset은 루트 디렉토리의 public에서 처리가능하다. public 안에 있는 것들은 절대 경로로 참조될 수 있다는 특징! 또한 구글 사이트 확인을 위한 robots.txt를 사용하는데 유용하다. 
2. 이미지 최적화를 해주는 컴포넌트가 있다. 
->브라우저가 지원되는 경우, 확장자를 Webp로 변환하여 전달하고 디바이스마다 크기를 재조정하여 보낸다. 
3. Head 컴포넌트로 각 페이지에 title 및 외부 script를 추가할 수 있다.
4. Script 컴포넌트로 외부 script를 최적화해줄 수 있다. Script 컴포넌트의 attr로는 strategy (언제 로드될 것인가), onLoad(로드된 이후 JS 코드 실행) 
5. next.js에 빌트인 css가 있다. 

### pre-rendering and data Fetching
중요한 개념 : **pre-rendering**
#nextDefault 각 페이지는 모두 pre-render가 기본 동작이다. 이 말인 즉슨 클라이언트에서 JS를 사용해서 HTML을 변경하는 게 아니라 next.js가 사전에 매 페이지에 대한 HTML을 만들어준다는 것이다. 이로 인해 SEO와 TTV가 좋아진다.  각각 만들어지는 HTML은 페이지에 대한 최소한의 JS 코드를 제공하는 것과 연관이 있다. 브라우저에 의해 페이지가 로드될때, JS 코드가 실행하고 상호작용할 수 있도록 만드는데 이것을 Hydration이라고 한다. 
- 나만의 언어 정리 Hydration : 페이지가 로드 되고 JS가 페이지의 상호작용을 덧입혀 완성하는 것.
-> js를 비활성화시키면 react는 "You need to enable JavaScript to run this app."을 보여주지만 next.js는 스타일이 덧입히지 않은 html이 보여진다.

#### pre-rendering 정리
1. initial load : 사용자가 웹사이트에 방문하면 서버로부터 만들어진 html을 보여준다. (TTV가 빠름)
2. hydration : 리액트 컴포넌트가 실행되고 상호작용 요소들이 활성화된다. 

##### Two forms of pre-rendering
1. Static Generation 
-> 빌드 타임에 HTML을 만든다. 그리고 매 요청마다 재사용이 된다. 
2. SSR 
-> 매 요청마다 HTML을 만든다. (서버 부담이 클 수 있겠다.)

![SSG|600](https://nextjs.org/static/images/learn/data-fetching/static-generation.png)

![SSR|600](https://nextjs.org/static/images/learn/data-fetching/server-side-rendering.png)

-> 개발 환경에서는 매 요청때 pre-render가 된다. SSG도 마찬가지. 베포 환경에서는 한번만 HTML을 만든다. 

#### Per-page Basis
next.js는 페이지 별로 pre-rendering 방식을 정할 수 있다. 페이지 별로 SSG 혹은 CSR 그리고 SSR로 구성할 수 있다. 현명한 방법은 대부분 SSG로 하고 상호작용이 많은 부분을 SSR로 하는게 좋다. 


##### SSR과 SSG 기준은? 
1. SSG : 공식 문서의 저자가 말하길 대체로 SSG를 사용하는게 좋다고 한다. 왜냐하면 내 페이지가 빌드시 HTML을 생성하는 동시에 CDN에 의해 제공될 수도 있다.
-> 마케팅 페이지, 블로그 , 이커머스 , 기술 문서

2. SSR : 유저에게 최신 정보를 보여줘야하는 페이지 같은 경우는 SSG가 적합하지 않다. 그럴 경우 SSR을 사용하는 것. 느리지만 최신의 정보를 제공할 수 있다는 장점이 있다. 이렇게 해도 되지만 pre-rendering을 하지 않고 'use client'을 활용해서 클라이언트 사이드 렌더링을 할 수도 있다. 

### SSG with and without Data
빌드시 외부 API를 이용하거나 외부 데이터를 사용할 경우를 위해 Next.js가 제공하는 것이 있다.  -> getStaticProps 13버젼에서는 이름이 다름. 이 함수 안에서 외부 데이터를 받고 빌드하게 됨. getStaticProps는 베포환경에서 빌드시 동작한다. 
-> V13부터는 fetch 옵션을 통해 getServerSideProps, getStaticProps 처럼 사용 가능하다. 
```tsx
export default async function Page() {
  // This request should be cached until manually invalidated.
  // Similar to `getStaticProps`.
  // `force-cache` is the default and can be omitted.
  const staticData = await fetch(`https://...`, { cache: 'force-cache' });

  // This request should be refetched on every request.
  // Similar to `getServerSideProps`.
  const dynamicData = await fetch(`https://...`, { cache: 'no-store' });

  // This request should be cached with a lifetime of 10 seconds.
  // Similar to `getStaticProps` with the `revalidate` option.
  const revalidatedData = await fetch(`https://...`, {
    next: { revalidate: 10 },
  });

  return <div>...</div>;
}
```


### SSR with and without Data
getServerSideProps를 사용하는 이유는 매 요청마다 해당 HTML에 최신화된 데이터가 있어야하는 경우이다. **TTFB**은 getStaticProps보다 느리다. 왜냐하면 서버가 매 요청마다 결과값을 내려줘야하기 때문. 또한 환경설정을 해주지 않는 이상 CDN에 캐시되지 않는다. 

### CSR 
데이터를 pre-render할 필요가 없다고 판단될때 CSR해줘도 된다. 
ex) 데시 보드와 같은 서비스에서는 적합. 대시 보드는 개인적인 서비스이고 SEO도 상관없어서 pre-render을 할필요가 없다. 하지만 데이터는 자주 바뀌어서 매 요청에 데이터를 불러오긴 해야한다. 이럴때 CSR을 사용하면 된다. 

### SWR 
CSR 사용할때 데이터 패칭은 SWR로 하는것을 추천한다. SWR은 캐싱, 재검증, 포커스 추적, 일정 간격으로의 다시 불러오기 등을 자동으로 처리한다. 


### Dynamic Routes
1. URL params에 따라 달라지는 페이지에 data-fetching을 하고 싶으면 getStaticPath와 getStaticProps를 사용하면 된다. 

#### summary 
다이내믹 라우트 안에 고정적인 데이터 넣는 방법
1. 리액트 컴포넌트가 페이지에 렌더되고 
2. getStaticPaths가 ID 리스트를 반환해야한다. 
3. getStaticProps는 id와 함께 데이터를 요청해야한다. 

### fallback (이부분 이해가 안가서 다른 사전 지식을 찾아야할 것 같다. )
getStaticPaths에서 fallback : false를 반환했는데 이게 뭐지?
fallback이 false이면 GSPs에서 반환하지 않은 모든 페이지 404 페이지 처리 
fallback이 True getStaticProps의 동작이 변경 
- GSPs로 반환된 경로 빌드시 HTML로 렌더링
- fallback이 blocking인 경우 새로운 경로는 gSPs를 사용하여 서버 측에서 렌더링되고 해당 경로에 대해 캐싱되어 나중에 다시 요청할때 한번만 실행된다, 


## 깊은 지식
1. js를 비활성화 하면 css가 입혀지지 않는다. 



## Next.js 렌더링 과정 
### Pre-Rendering
1. 서버 사이드에서 [ReactDomServer.renderToString()](https://react.dev/blog/2022/03/08/react-18-upgrade-guide#deprecations)이라는 함수를 사용해 HTML을 문자열로 가지고 온다. 
2. 클라이언트로 Pre-rendering한 html을 전달해준다. 사전에 클라이언트 단에서 렌더링 방식을 정할 수 있습니다. 
3. 브라우저는 매 request에 응답으로 prerendering한 html을 받습니다. 이때 화면에 렌더링을 시작하고 html 문서에 있는 js 파일을 로드합니다. 이후 클라이언트에서 ReactDom.render 함수를 통해서 React Element를 렌더링하고 이후 hydration을 통해서 interactive한 페이지로 완성시킵니다. 


참고
1. https://funveloper.tistory.com/164

# Version 12
1. [[next page]]
2.  [[getStaticProps]]
3.  [[getServerSideProps]] 오늘 이해한다 (1.10)
4. [[next_seo]]
5. [[next.Image]]

# Version 13
next.js source code : https://github.com/vercel/next.js/
1. 렌더링 원리 : [[next.js rendering]]
2. 서버 컴포넌트와 클라이언트 컴포넌트 : [[server component]] , [[client component]]


## 중요한 개념 re-rendering 



### 생각의 연결고리
분야 : [[difference framework and library]]

키워드 :

관련있는 메모 :
