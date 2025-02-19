---
aliases: [기본기]
tags : 
---
Up : [[HOME 🌎]]

출처 : 공식 문서
저자 : 
URL : https://ko.reactjs.org/docs/thinking-in-react.html
정리 : 

# 1단계: UI를 컴포넌트 계층 구조로 나누기

컴포 넌트 기준 : 단일 책임 원칙

state는 오직 상호작용을 위해, 즉 시간이 지남에 따라 데이터가 바뀌는 것에 사용합니다. (정말 함축적으로 사용해야하는 거구나)

애플리케이션을 올바르게 만드릭 위해서는 애플리케이션에서 필요로 하는 변경 가능한 state의 최소 집합을 생각해야한다.
필수적으로 생각해야하는 것 : [[중복 배제원칙]] 

- 페이지 내 데이터 생각해보기 
	- 에디터 페이지
		1. 어떤 선택 항목을 선택했는지
		2. 설문 페이지에 선택들이 들어가 있는지
		3. 관리자가 입력한 질문 및 선택 항목 질문

최소한으로 필요한 state가 무엇인지 찾아내는게 관건.

- state가 어디에 있어야할 지를 찾기
	1. state를 기반으로 랜더링하는 모든 컴포넌트를 찾는 것
	2. 공통 소유 컴포넌트를 찾는 것
	3. 공통 혹은 더 상위에 있는 컴포넌트가 state를 가져야 합니다.
	4. state를 소유할 적절한 컴포넌트를 찾지 못하였다면, state를 소유하는 컴포넌트를 하나 만들어서 공통 소유 컴포넌트의 상위 계층에 추가하세요.


예시)  

![[스크린샷 2022-09-30 오후 12.05.40.png]]

![[스크린샷 2022-09-30 오후 12.05.57.png]]

1. productTable은 state에 의존한 상품 리스트 필터링!
2. searcbar는 검색어와 체크 박스의 상태를 표시
3. 공통 소유 컴포넌트는 최상위 컴포넌트를 말하고 있다.
	(검색어와 체크 박스의 체크 여부를 가지는 것이 타당.)
	{filterText: '', inStockOnly: false} 를 FilterableProductTable의 초기 상태로 반영







### 생각의 연결고리
분야 :

키워드 :

관련있는 메모 :
