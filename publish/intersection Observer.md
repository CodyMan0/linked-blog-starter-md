출처 : https://developer.mozilla.org/en-US/docs/Web/API/Intersection_Observer_API


사용처 
- 이미지 지연 로딩 혹은 페이지가 스크롤될때 보여질 콘텐츠 
- 무한 스크롤 사용시 필요한다. 
- 광고 수익을 계산할때 필요하다

intersection Observer는 기대하고 있는 코드가 어떤 엘리먼즈를 접촉하거나 이탈할때  콜백 함수를 등록한다. 이렇게 함으로써 메인 쓰레드의 부담을 줄여주고 이벤트 루프로 위임한다. 하지만 Intersection Observer를 통해 알 수 없는 것은 겹쳐진 정확한 픽셀단위 위치와 유저의 정확한 위치를 알 수 없다는 것. 그러나 대충은 알 수 있다. 


## 컨셉
Intersection Observer API는 다음 상황 중 하나가 발생할 때 콜백을 구성할 수 있게 해줍니다:

1. 타켓 요소가 뷰포트에 들어올때
2. 부표트를 벗어날때

각각 콜백함수를 호출할 수 있도록 설정할 수 있다. 


## 예제 코드
```js
const options ={
	root : null,
	rootMargin: '0px',
	threshold: 1.0,
}

const callback = () => {
	console.log('Entries', entries)
} 

const observer = new IntersectionObserver(callback, options)

observer.observe(document.querySelector('#target-element1'))
```

root : 대상 객체 사용되는 View Port. default : null
rootMargin : root 요소의 여백. 
threshold는 가기성 퍼센티지. target 요소가 어느 정도로 보일 때 콜백을 실행할지 결정한다. (1.0은 완전히 다 보이면 실행, 0이면 1px이라도 보이면 콜백 함수가 실행된다. )


## 딥 다이브 
IntersectionObserverEntry 프로퍼티의 배열 value를 뜯어보자
1. boundingClientRect 
2. intersectionRatio
3. intersectionRect
4. isIntersecting
5. isVisible
6. rootBounds
7. target
8. time

