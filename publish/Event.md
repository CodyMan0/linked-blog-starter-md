
# Event

자바스크립트는 이벤트 중심적 프로그래밍이다. 
왜? 프로그램의 흐름을 이벤트 중심으로 제어하고 있기 때문에 

## 이벤트 핸들러 등록

event handler란 event가 발생할때 부라우저에 의해 호출될 함수를 말한다.

### 이벤트 사용 자료에 의한 추천
> attribute(inline) < property < addEventListener

react attribute?

### 이벤트 핸들러 어트리뷰트 방식

#Q 함수 참조를 할당하는지 함수 호출(문)을 할당하는지가 중요한가? -> 실행컨텍스트? -> () 호출 Return -> 함수 자체를 넣어놓으면 콜백시 실행!! 

#Q 이벤트 핸들러 어트리뷰트 방식이 뭐지? angluar, react, vue는 이 방식으로 이벤트를 처리한다고 한다. 

-> **리액트 Jsx문법을 사용**  [[JSX]]는 js를 html로 파싱하기에 관심사 분리를 할 필요가 없다.

#Q removeEventListener를 언제 쓰지? -> 리액트를 사용하면서 자바스크립트 RemoveEventListener를 잘 모르는 것 같다. 

### 이벤트 핸들러 프로퍼티 방식
어트리뷰트 방식으로 인해 html,css와 js가 섞이는 문제를 방지 할 수 있으나 프로퍼티에 하나의 이벤트 핸들러만 바인딩할 수 있다는 단점이 있다. 


###  addEventListener 메서드 방식

addEventListener 메소드를 이용하여 대상 [[DOM]] 요소에 이벤트를 바인딩하고 해당 이벤트가 발생했을 때 실행될 콜백 함수(이벤트 핸들러)를 지정한다.
![[스크린샷 2022-12-31 오전 10.23.03.png]]

생략하거나 False면 -> 버블링 단계에서 이벤트 캐치 -> true면 캡처링 단계에서 이벤트를 캐치
[[capturing and bubbling]]

addEventListener는 이벤트 핸들러 프로퍼티에 바인딩 영역에 영향을 주지 않는다!

이전에 event를 사용했던 방식보다 좋은 점을 정리해보면
-   하나의 이벤트에 대해 **하나 이상의 이벤트 핸들러를 추가**할 수 있다. 어떻게? -> **removeEventListener**이 등장하는 이유 
-   캡처링과 버블링을 지원한다. 어떻게? 마지막 인자
-   HTML 요소뿐만아니라 모든 DOM 요소(HTML, XML, SVG)에 대해 동작한다. 브라우저는 웹 문서(HTML, XML, SVG)를 로드한 후, 파싱하여 DOM을 생성한다.


```js
const button1 = document.querySelector("button");

  

button1.addEventListener("click", function () {

console.log("11111111");

});

  

button1.addEventListener("click", function () {

console.log("22222222");

});
```
![[스크린샷 2022-12-31 오전 10.33.40.png|300]]




### 차이
1. addEventListener는 하나의 html에 여러가지 이벤트를 등록시킬 수 있다. 등록된 순서대로 호출된다. -> remove 

2. add는 remove로 이벤트를 삭제할 수 있지만 property로 이벤트를 할당한 애들은 null을 재 할당하는 방식으로 제거








## 이벤트 객체 
말 그대로 이밴트가 발생할때 생기는 객체 

- 모든 이벤트 간에 공통적으로 생기는 프로퍼티
type
target : 이벤트를 발생 시킨 DOM 요소
currentTarget
eventPhase
bubbles
cancelable
defaultPrevented
isTrusted
timeStamp

#Q. target과 currentTarget의 차이 : currentTarget은 eventHandler 붙어있는 돔요소


## 이벤트 핸들러 내부의 this 
### 1. inline's this : window 
```js
<button onclick="foo()">Button</button>
<script>
    function foo () {
      console.log(this); // window
    }
</script>

```

### 2. property 's this : 이벤트가 바인딩된 요소

```js
<button class="btn">Button</button>
 
<script>
    const btn = document.querySelector('.btn');
 
    btn.onclick = function (e) {
      console.log(this); // <button id="btn">Button</button>
      console.log(e.currentTarget); // <button id="btn">Button</button>
      console.log(this === e.currentTarget); // true
    };
</script>
```

이밴트 핸들러 내부 this = currentTarget

### 3. **addEventListener 방식**

addEventListener 메소드에서 지정한 이벤트 핸들러는 콜백 함수이지만 이벤트 핸들러 내부의 **this는 이벤트 리스너에 바인딩된 요소(currentTarget)**를 가리킨다.

```js
<button class="btn">Button</button>
 
<script>
    const btn = document.querySelector('.btn');
 
    ul.addEventListener('click', function (e) {
      console.log(this); // <button id="btn">Button</button>
      console.log(e.currentTarget); // <button id="btn">Button</button>
      console.log(this === e.currentTarget); // true
    });
</script>
```

프로퍼티 방식과 동일하다
[[this-binding]]










## 이벤트 전파 event propagation 
[[capturing and bubbling]]



## 이벤트 위임

