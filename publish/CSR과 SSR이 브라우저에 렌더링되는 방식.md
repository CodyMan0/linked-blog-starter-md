## 전통적인 브라우저 렌더링 방식
[[브라우저 렌더링 과정]]



## SSR과 브라우저 렌더링
> SSR은 말 그대로 서버에서 미리 HTML을 파일을 만들어 클라이언트로 응답해주는 방식 

전통적인 브라우저의 렌더링 방식과 동일 
1. HTML 파싱하여 DOM 트리를 만든다 
2. CSS 파싱해서 CSSOM 만든다
3. 두개를 결합하여 render tree를 만든다 
4. render tree를 기반으로 layout(위치 계산) 및 paint(픽셀로 그려주는 작업)이 이루어진다.
5. 자바스크립트 엔진으로 제어권이 넘어간다.
6. **중요**한 것은 이 당시에 UI는 완성되어 있다는 것이 핵심


**프레임워크** : [[Next.js]]

https://velog.io/@surim014/how-next.js-works#%EB%A0%8C%EB%8D%94%EB%A7%81%EC%9D%B4%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%BC%EA%B9%8C%EC%9A%94
SSR https://www.howdy-mj.me/next/hydrate
1. 웹사이트 방문하면 서버에서 필요한 html을 만들게 되고 동적으로 미세하게 제어할 수 있는 js와 함께 클라이언트로 내려준다. 
장 -> 당연히 TTV가 빠르다. 효율적인 SEO
단 -> 서버 과부화 TTI가 느리다. 




## AJAX의 등장이후 CSR 브라우저 렌더링과 가상돔 
https://www.youtube.com/watch?v=kP-H1GXD_nI
**라이브러리** : [[react MOC]]

> CSR은 서버로부터 css,js link만 있는 빈 HTML파일을 전송받아 클라이언트 사이드에서 불러오는 방식

전통적인(MPA) 브라우저 렌더링과 SSR의  브라우저 렌더링 방식과 거의 동일 
1. HTML 파싱하여 DOM 트리를 만든다 
2. CSS 파싱해서 CSSOM 만든다
3. 두개를 결합하여 render tree를 만든다 
4. render tree를 기반으로 layout(위치 계산) 및 paint(픽셀로 그려주는 작업)이 이루어진다.
5. 자바스크립트 엔진으로 제어권이 넘어간다.
6. 이 당시 UI가 미완성되어있고 JS에서 UI 요소를 하나하나 **동적**으로 생성하며 그려준다. 

### react 
리액트는 HTML이 하나인 대중적인 SPA 라이브러리로서 전통적인 MPA 웹페이지과 다르게 페이지 이동시 깜빡임이 없다는 특징이 있다. 

맨 처음 유저가 웹사이트에 도착하면 
1. 단일 HTML 
2. 비교적 큰 사이즈 react JS 프레임워크 소스 코드 
3. static files 전달 

> CRA로 만든  리액트 웹 어플리케이션은 페이지에 방문하면 네트워크에 어떤 것들을 받아올까? 

1. localHost (html)
2. bundle.js ( react 모든 코드들이 webpack이라는 모듈 번들러로 번들돼서 하나의 js로 설정)
3. styled-component

styled-components를 사용하면 JS 코드로 작성되고 이말인 즉슨 런타임 중에 실행된다는 것. 그래서 cssom 트리에 반영되지 않고 페이지가 로드되는 동안 동적으로 생성된다. 
styled-components는 SSR을 통해 스타일을 사전에 렌더링한다고 한다. 서버에서 JS 코드에서 정의된 스타일에 따라 css 규칙을 생성한다. 

현재 난[[styled-component]]의 원리를 모르는 것 같다. 
-> 기존 DOM을 만들때 CSS는 외부 css나 scss를 link 태그로 연결한 후, id와 class 식별자를 활용해서 연결해주었는지 styeld-components를 활용하여 전역적인 스타일을 없애고 컴포넌트 내부로 옮겨 namespace의 충돌을 막는다.


JS로 기존의 돔이 수정될 경우, 리페인트 레플로우가 발생한다. 이떄 불필요한 리렌더링이 발생하면 성능에 악영향을 미치는데 이러한 문제를 극복하기 위해 react에서는 가상돔을 사용하여 변경된 부분만 반영해주는 방식으로 렌더링을 최적화한다. 



## 핵심 
- SSR 방식은 CSR 보다 TTV(유저가 렌더링된 화면을 보는데 까지 걸리는 시간)이 짧다. 반대는 역이다.
- SSR 방식은 TTI(유저와 상호작용할 수 있는 기능들을 다소 늦게 활성화가 된다. )



## SSR
[[SSR]]
## CSR
[[CSR and SSR]]


## SSG
[[SSG]]
[[SSG's Ecosystem]]