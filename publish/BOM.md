 ### 2022-07-22 18:05  

## 주제 : BOM이 무엇인가!
----

BOM은 브라우저를 객체화하여 자바스크립트로 제어할 수 제공해주는 API 

- Browser Object Model. 브라우저 자체를 다루기 위한 API 전역객체 Window의 프로퍼티에 속한 객체들이 이에 속한다. 돔에 진입하기 위한 진입점.

특징 : 최상위 노드 

window
document
history
location
screen
navigator



### 사용자와 커뮤니케이션 하기 
window의 대표적인 전역 객체를 살펴보면 alert (확인), confirm (확인과 취소 버튼이 있고 그로인해 true and false 리턴값), prompt( 사용자의 typing이 리턴값)

### location 객체
- Location 객체는 문서의 주소와 관련된 객체로 Window 객체의 프로퍼티다. 이 객체를 이용해서 윈도우의 문서 URL을 변경할 수 있고, 문서의 위치와 관련해서 다양한 정보를 얻을 수 있다.


### Navigator 객체
자바스크립트가 실행되고 있는 [[working process of browser]]의 제품명, 버젼을 알 수 있음. 그것을 통해 우리의 코드가 각 브라우저에서 적용이 되는지 알아보게 해주는 브라우저 이름. 
[[cross-browsing issue#개발자 도구를 쓰는 이유중에 말씀하심]]


- useAgent : 브라우저가 서버측으로 전송하는 USER - AGENT HTTP 해더의 내용.



## 나만의 언어로 정리
BOM은 웹페이지 내용을 제외한 브라우저의 각 요소들을 객체화시킨 것이고 전역 객체 [[windowProperty]]와 관계가 있다.


### 출처(참고문헌)
1. 얄코 https://youtu.be/1ojA5mLWts8
### 연결문서
- 
