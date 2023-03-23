# react-router,scss(LN)

1. SPA 가 무엇인지 설명할 수 있다.

: 하나의  HTML로 이루어진 웹 어플리케이션 

2.  react-router-dom을 이용해 Router Component를 구현할 수 있다.

3.  `react-router-dom`을 이용해 `Routing`을 하는 방법 2가지와 차이점에 대해 설명할 수 있다.
큰 흐름
1. router.js 로 라우팅 기능을 만들어서 index.js로 export하는 방법
2. Link to 사용
3. useNavigate (hook) 사용)

link와 useNavigate hook 차이
- useNavigate은 백엔드 API로 데이터를 전송하는 작업을 한 뒤 ==페이지를 이동하거나 userData의 인증 혹은 인가가 필요한 경우==, 혹은 로그인 작업 이후 응답 메시지에 따른 분기 처리를 해야 하는 상황일 때, useNavigate를 사용하는 것이 좋습니다. 
- ==페이지를 이동하기 때문에, 조건 없이 페이지==를 이동할 때 적합

5.  `<Link> Component` 와 `<a> tag` 의 차이점에 대해 설명할 수 있다.
-> a는 매법 새로운 페이지를 요청해서 받아오는 반면  link 컴포넌트를 통해 변환된 a 태그는 실제 서버에 요청을 보내지 않고 단지 url만 변경합니다. 

5.  `css 전처리기`의 역할에 대해 설명할 수 있다.
-> **실제 실행 전에 처리**를 해줌으로 브라우저가 읽을 수 있는 css 파일로 변환 시켜주는 역할을 수행한다.
6.  `sass`에서 제공하는 문법을 이용하여 `css`파일을 `scss`파일로 변환할 수 있다.



### 연결문서
- [[react-router and sass (FN)]]
