
Up : [[knowledge_MOCs]]

출처 :
저자 :
URL : [http method 정리 블로그](https://inpa.tistory.com/entry/WEB-%F0%9F%8C%90-HTTP-%EB%A9%94%EC%84%9C%EB%93%9C-%EC%A2%85%EB%A5%98-%ED%86%B5%EC%8B%A0-%EA%B3%BC%EC%A0%95-%F0%9F%92%AF-%EC%B4%9D%EC%A0%95%EB%A6%AC)
인용 :  

# http method란
서버에 주어진 리소스에 수행하길 원하는 행동을 지정하는 것. 

주요 메소드
1. GET : 리소스 조회
2. Post : 요청 데이터 처리, 주로 등록
3. PUT : 리소스를 덮어쓰거나(전체변경) 해당 리소스가 없으면 생성
4. PATCH: 리소스 부분 변경
5. DELETE: 리소스 삭제

기타 메소드
1. HEAD : GET과 동일하지만 메세지 부분을 제외하고 상태줄과 헤더만 반환
2. OPTIONS:대상 리소스에 대한 통신 가능 옵션을 설명
3. CONNECT: 서버에 대한 터널을 설정
4. TRACE: 대상 리소스에 대한 경로를 따라 메세지 루프백 테스트 수행 

## 조회 : GET vs POST
get 메소드는 ==캐싱==이 가능하기에 데이터를 조회할땐 post보다 get을 사용하는 것이 유리하다 

## 생성 : post
Content-type 헤더 종류 알자
1. application/json : TEXT,XML,JSON 데이터 전송시 사용
2. multipart/form-data : 파일 업로드와 같은 바이너리 데이터 전송 시 사용, 다른 종류의 여러 파일과 form의 내용 함께 전송 가능
3. application/x-www-form-urlencoded : Form의 내용을 HTTP메세지 바디를 통해 전송, 전동 데이터를 URL encoding 처리

## 수정 : PUT vs PATCH
만일 요청 메세지에 리소스가 있으면 덮어쓰고 없으면 새로 생성 없으면 POST와 같이 신규로 생성 

만약 일부만 수정하고 싶을때는 PUT이 아닌 PATCH를 사용해야한다.

# HTTP 메소드 속성
![[Pasted image 20230206134946.png]]

## 안전한가
호출해도 리소스가 변경되지 않는 성질

## 멱등성을 가질 수 있는가?
http 매서드가 멱등성을 가진다는 것은 1,2를 만족할때 
1. 동일한 요청을 한번 혹은 여러번 보내도 같은 효과를 가지고
2. 서버의 상태도 동일할때
## 캐시가 가능한가
응답 리소스를 캐싱해서 효율적으로 사용할 수 있는가 
서, GET HEAD 메서드는 캐시가 가능하기 때문에 브라우저에서 리소스를 임시로 보관할 수 있고, 나머지 메서드들은  구현의 복잡성 혹은 유지의 어려움 때문에 캐시를 이용하지 않는다고 생각하면 된다.





### 생각의 연결고리
분야 :

키워드 :

관련있는 메모 :
