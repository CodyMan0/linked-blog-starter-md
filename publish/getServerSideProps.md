지식 총동원 getServerSideProps 정리해보려고 한다.

우선 공식 문서! 

getServerSideProps 함수를 페이지에서 export하면 프레임워크가 알아서 함수에 의해 반환된 데이터를 활용한 요청을 페이지에서 pre-render를 해준다. 

여기는 오케이

그럼 pre-render가 뭐지? 우선 당연히 사전에 미리 render해주는 것이겠지만 조금 더 제대로 보면

미리 HTML을 만드는 기능 
-> 초기로드에 미리 생성된 Html 표시하고 Hydration이 이루어진다. 컴포넌트들이 초기화되고 버튼들이 눌러지는 것 
![[스크린샷 2023-01-10 오전 10.10.09 1.png|400]]
## pre-rendering의 방식 두가지
1. Static Generation : Html을 빌드타임에 생성해 두고 요청시마디 재사용하는 방법
2. Server-side-Rendering : 요청시마다 html을 생성해주는 방법

항상 같은 화면만 나오는 페이지라면 Static Generation 

