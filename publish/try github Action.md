1. prefix에 .github/workflows를 action에서 받는다.
2. yml 파일 알아야한다.
	-> name , uses , with , run의 차이점을 알아야한다. 
	-> peaceiris/actions-gh-page@v3
	[[env 찾아보기]]
	-> .env.produnction 관련한 궁금증 
	-> .env를 만드는 목적 github상에 드러내지 않고 숨기기 위해서인데 .production 접미사를 사용하면 github에 베포할때 main 브랜치에 드러난다. 그래서 준호님이 설명한 방법
	-> echo 'scret 이름' >> .env.production

3. push와 pull request 가 있는데 우선 push만 남겼다 왜? 정리 나중에 

4. ![[스크린샷 2022-12-21 오후 3.10.35.png]]
-> 베포하니깐 페이지를 가지고 오지 못한다. 
-> process.env.PUBLIC_URL 
-> 비트 깃허브 베포 


-> app.js 베읻스 유알엘 삭제
-> vite config.js

-> base: 'kakaoGroupPage',

-> base: 'codyman0.github.io/kakaoGroupPage',


-> 왜 접근이 안되지? 

-> base: '/kakaoGroupPage/',

-> 변화되는 부분이 있어야 publish가 된다. 

-> github는 라우팅 기능을 제공해주지 않는다!!?

-> github 404페이지 제공 원리 정리해보자 

-> 
![[스크린샷 2022-12-21 오후 4.18.31.png]]

token 문제


-> 메인 브랜치에 바로 푸쉬 되지 않도록 브랜치 설정을 해보자 

