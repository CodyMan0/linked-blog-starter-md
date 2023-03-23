
Up : [[knowledge_MOCs]]

출처 : 공식 문서 
저자 :
URL : https://beta.nextjs.org/docs/rendering/fundamentals
인용 : 

코드가 렌더되는 환경은 client와 server가 있다. 

- client : 유저 장치의 브라우저 
- server : app의 코드를 저장해놓은 데이터 컴퓨터, client로부터 요청을 받고 약간의 연산 그리고 적절한 응답을 줄 수 있도록 설계


## 클라이언트 컴포넌트와 서버 컴포넌트 

app 디렉토리는 서버 컴포넌트가 적용된다. 클라이언트로 전달되는 js의 수를 줄이도록 설계 

서버, 클라이언트 컴포넌트를 적절하게 사용할 수 있다. 서버 컴포넌트를 child 혹은 props로 client 컴포넌트로 넣어줄 수 있다. 

리액트가 선언적으로 두 환경을 병합시켜준다고 한다. 


## 서버에서 정적이며 동적 랜더링
CSR SSR이외에도 서버에서 static and dynamic rendering을 지원해준다. 
### static rendering
빌드타임에 prerender이 된다. 이렇게 생성된 데이터는 캐시가 되고 재사용이 가능해진다. revalidate가 되어진다. 
이 개념은 SSG와 ISR과 동일하다고 한다. 

### Dynamic rendering 








### 생각의 연결고리
분야 :

키워드 :

관련있는 메모 : [[react MOC]]
