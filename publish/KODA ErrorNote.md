

==ref와 state 차이 정리==

-> React 컴포넌트에서 `ref` 를 사용하기 위해서는 `forwardRef` 를 사용해야합니다. `forwardRef` 를 사용하여 더 아래의 컴포넌트에 `ref` 를 전달할 수 있게됩니다.

``` jsx
  

const MultipleSingle = forwardRef(function MultipleSingle(

{ sortIndex, onChange, onBlur, name, label },

ref

) {

return (

<div>

<GlobalQuestion

sortIndex={sortIndex}

type={QUESTION_ARRAY_TYPE.multipleSingle}

>

<MultiInput />

<MultiInput />

<MultiInput />

<MultiInput />

</GlobalQuestion>

</div>

);

});

  

export default MultipleSingle;
```
이렇게 하니깐 됐다... 

-> 이렇게 안해도 useFormContext 사용하니깐 더 쉽게 됐다

10.  클릭 이벤트에 list 갯수에 따른 숫자를 더하기 해줄 setState를 함수형 업데이트로 했는데 에러나 계속 난다.
![[스크린샷 2022-10-01 오전 10.44.58.png]]
-> ![[스크린샷 2022-10-01 오전 10.49.05.png]]
아 젠장... props 이름을 안바꿨어서.. 바꿔줬다 해결! 

11.  데이터 구조가 아래와 같은데

![[스크린샷 2022-10-01 오전 11.50.46.png]]

첫번째 0 , 1, 2,3은

```Jsx
(

formList.map((form, idx) => (

<RealSurvey key={idx}>

{QUESTION_ARRAY(idx + 1)[form[0][1]]}

</RealSurvey>

))

)
```
맵으로 한커품 벗겨졌고 이제 0의 아이디에 type에 접근하고 싶다. 이것을 해야 목으로 받아왔을떄도 가능할 것같은데 


12. setFormList is not iterable...
이 에러가 가장 오래 걸리는 것 같다. 
왼쪽에 옵션 박스를 클릭하면 ![[스크린샷 2022-10-01 오후 2.01.48.png]]
옵션을 클릭하면 저 양식에 따라 데이터가 가도록 하고 싶은데...  계속 iterable하다고 나온다. 왜 일까? 

-> 우선 반복때문이라는 것은 알았는데 

후... 3시간만에 찾은 블로그,

출처 : https://junior-datalist.tistory.com/70
![[스크린샷 2022-10-01 오후 3.55.25.png]]
이놈의 함수형 업데이트 때매 내가 미친다... 정확히 알게 되는 것 같다...

13. 공통 질문인 GlobalQestion이라는 컴포넌트는 모든 질문들에서 Import해서 사용하고 있는데 하나의 질문이 하나의 객체이다. 그런데 하나의 질문에 값을 넣으면 다른 값에서도 동일한 나온다... 이걸 이름으로 분류를 해줘야하는데 어떻게 해줘야할까? 참고로 이 컴포넌트 위해서 map을 사용해서 ... 흠

![[스크린샷 2022-10-02 오전 11.50.30.png]]

정리해보자 
1. 현재 상황
-> 왼쪽 옵션 박스에서 해당하는 타입의 번호를 누르면 오른쪽 surveyEditor에 타입에 따른 질문 component가 뿌려지는 상황
-> 질문 component 안에는 global input이라는 컴포넌트를 공유하고 있다. 그래서 질문들의 value가 다 같은 문제가 발생

-> 구조적으로 바꿀 것인지?
-> 


2. 원하는 상황 
-> 하나의 질문은 formData 라는 배열 안에 있는 객체이다. 그리고 하나의 질문안에 실제 제목은 각 객체 안에 question이라는 키값으로 들아가야한다. 


생각 방향
1. 아예 왼쪽 박스를 클릭했을때 나오는 컴포넌트로 가서 거기서 useForm을 불러와서 name을 설정해줘야할까? 
2. useFieldA

GlobalQuestion 컴포넌트에서 질문들에 대한 네임을 번호대로 하니깐 됐다! ![[스크린샷 2022-10-02 오후 12.17.48.png]]
근데 새로운 문제.
![[스크린샷 2022-10-02 오후 12.19.14.png]]
기존에 있던 형식의 객체가 초기화되는 것 같다...??? 

아!! 첫번째 데이터만 defaltValue로 들어가는 것 같다. 


아!!  다른 문제 원래 됐었던 것 같은데 ... 앤터를 치면 0번째 데이터만 들어가고 나머지에는 안들어가는 현상이 있다. 다시 생각해봐야한다. 

확인해보기 ... 원래 안되고 있었던 것

useForm의 DefaultValue 때문에 첫번째 0 번째만 들어간 던것...

-> 그럼 모든 폼 데이터를 반영해서 어떻게 보낼 수 있지/?

-> useForm 을 통해 만든 데이터를 스테이트에 담아야하나? 
	-> 아니다 !! 자동으로 submit 누르면 Data라는 스테이트가 만들어지는 것을 볼 수 있다. 


## 지금 해야하는 것
데이터를 보내야하는 것. id값과 type들이 submit 눌렀을때도 들어가야한다. 



선택 항목의 질문을 늘리는 것은 UseFieldArray를 사용하자 

2. 내가 하고 싶은 것
	-> 


타입에 따라서 애들을 보여주면 될 것 같다!!??

그럼 아이디 값이 바뀌나? 

안되네.....

**-> 크흠 어떻게 해야하는거지?** 얘기해보기 
-> 윤국님이 사용했던 방식들 찾아보기 

탬플릿 UI 어떻게 할껀지



-> useForm 안에서 제어 인풋과 ㄹ비제어 인풋 공부하기
-> image 박스 탬플리셍 따른 인풋은 비제어로 관리하기.



19 . controlled or uncontrolled input의 차이를 이해하자 

출처 : https://ko.reactjs.org/docs/uncontrolled-components.html



# 보류 
1. mock.formData를 맵을 돌려서 하나씩 Question_array라는 함수를 통해서 Type이 1 -> 1의 컴포넌트를 보여주는 식으로 하는데... 
	mock.formData 안에 있는 질문들과 option들을 사용해서 뿌려주고 싶은데 지금 함수안에 인자로 넣어도 사용이 안되고 인자의 순서를 바꾸니 인덱스가 사용이 안되고... 어려움이 있따. 

-> 가변 인자라는 개념을 정확히 이해하게 되었다. 자바크립티느는 인자를 몇개를 넣던 받는 함수에서 ...args 하면 다 사용할 수 있다는 것을 알았다!! 


20 . useFieldArray를 사용하는데 ... fields에 추가가 되지 않는 현상이 있다. 

20-1 20번을 알려면 FormProvider를 정확히 알아야한다...
-> 1. Controller를 

출처 : https://velog.io/@leitmotif/Hook-Form%EC%9C%BC%EB%A1%9C-%EC%83%81%ED%83%9C-%EA%B4%80%EB%A6%AC%ED%95%98%EA%B8%B0#depth%EA%B0%80-%EC%9E%88%EB%8A%94-%EA%B0%92-%EA%B5%AC%EC%A1%B0%EB%8A%94-%EC%96%B4%EB%96%BB%EA%B2%8C


defalutValue와 ref? ![[스크린샷 2022-10-03 오후 12.07.23.png|500]]
컨트롤러를 내가 잘 모르고 있어서 useFieldArray를 사용하는데 있어서 어려움이 있는 것 같다. 


해결하기 위해서 한 것
1. MultiSignle 에서 useFormContext를 useForm으로 바꾸주었다.
2. GlobalQuestion에서 register로 받았던 것을 useFormContext로 바꿔줌 



22. usefieldarray fields not updating 이 현상을 겪고 있다.

23 . formData를 보낼떄 json parsing error가 나온다.
왜? -> 

24. 
Access to fetch at 'http://10.133.58.207:8000/editor/made' from origin 'http://localhost:3000' has been blocked by CORS policy: No 'Access-Control-Allow-Origin' header is present on the requested resource. If an opaque response serves your needs, set the request's mode to 'no-cors' to fetch the resource with CORS disabled

출처 : 
1. https://evan-moon.github.io/2020/05/21/about-cors/
왜??

해결 방법 
1. 출처를 알아낸다. (우리는 브라우저의 개발자 도구의 콘솔에서 `Location` 객체가 가지고 있는 `origin` 프로퍼티에 접근함으로써 손 쉽게 어플리케이션이 실행되고 있는 출처를 알아낼 수도 있다.)
나의 출처 : http://localhost:3000

3가지 방법 
1. ### Preflight Request

## 'Content-Type': 'application/json',

body: JSON.stringify({ data }), 하니깐 content-type이 있는데도 cors 문제가 해결!!

==그리고 JSON.stringify(data)로 객체를 벗기니깐 해결==

연관 [[SOP의 예외 조항인 CORS 정책]]



25. 이미지를 useForm안의 데이터로 녹여야한다. 
useFomr으로 이미지 업로드 하는 것 조금 찾아보기 

==Q.== 
-> base 64 를 통해서 인코딩을 해서 보내야하는지?
-> 중간에 이미지만 api로 보내는 방법으로 ? 
	-> 문제: 여기서 보낼때 밖에 폼도 같이 보내져서 에러가 발생


27. ![[스크린샷 2022-10-04 오후 3.19.49.png]]
다음으로 가기 눌렀을때 post 1번만 호출해야한다.
왜? 두개가 같은 페이지인데? 두번 보내지니깐 다른 설문지로 인식하는 에러가 생긴다. 

-> 다음으로 가기 눌렀을떄 폼이 submit이 안되면 좋겠는데....
**-> button을 p로 바꾸니깐 됐다**

28. 
![[스크린샷 2022-10-04 오후 3.50.29.png]]

근복적인 문제
저장하기 눌렀을때 상위 컴포넌트에 있는 useForm이 submit 되는 문제가 있는 것.

망고님한테 물어봐서 알게 된 것!!!!

확인해보자 지금 ==styledComponent의 버튼의 기본 값은 submit!!!!!!==
그래서 스타일드 컴포넌트로 만든 버튼을 눌렀을때는 form이 보내지지 않았었는데 내가 그냥 만든 button의 타입은 자동으로 submit이었다. 그래서 저장하기 버튼을 눌렀을때 폼이 보내지는 것이었다!!!!!!!!

-> 제일 끝에 있는 랜딩페이지 URL 입력하는 곳에 유효성 검사를 추가하여 인풋을 작성하지 않으면 보내지지 않게 하면 된다!!! 

-> 다음으로 가기를 눌러서 보여지는 거라 먹히지 않는다.



근본적인 문제가 해결되면 하고 싶은 부분 
다음으로 가기 눌렀을때 저장하기에 있는 함수가 호출하게 하고 싶다.
어떻게 하면 좋을까요?




29. 불변성을 지키면서 휴지통 기능 살리기
![[스크린샷 2022-10-05 오전 10.56.10.png]]

Undefined가 있는 상태에서 map을 돌려서 생기는 상황

``` jsx
{formList?.formData?.length > 0
```
옵셔널 체이닝 하니깐  해결은 됐는데 새로운 문제 

![[스크린샷 2022-10-05 오전 11.09.21.png]]

옵셔널 체이닝(optional chaining) `?.`을 사용하면 프로퍼티가 없는 중첩 객체를 에러 없이 안전하게 접근할 수 있습니다.

![[스크린샷 2022-10-05 오후 12.58.31.png]]

추가했을떄는 이렇게 만드는데...
삭제하고 난 이후에 받는 데이터는 

```js
const onRemove = id => {

setFormList(formList.formData.filter(form => form.id !== id));

};

```

같은 console.log(formList)
![[스크린샷 2022-10-05 오후 1.08.30.png]]
근데 삭제하고 나면 FormData 만 사라져야하는데 모드 사

![[스크린샷 2022-10-05 오후 1.22.22.png]]
미쳤다... 됐다!! 


30. 클릭했을때 number state를 증가시켜줌으로써 Id 값을 부여했는데 그러다보니 템플릿이 들어왔을땐 클릭하지도 않았기 떄문에 id state는 0이어서 추가했을때 아이디와 삭제했을때 id 값이 달라서 기능을 하지 않는다. 
Q. 그럼 어떻게 하면 될까?



31. react 서버로부터 이미지 보여주기
![[스크린샷 2022-10-05 오후 3.33.06.png]]

 base64로 디코딩, 인코딩 등등 별짓을 다해봤으나 실패
https://webcorgi.tistory.com/40
==공부해보기==

싱글 인풋일 경우 어떤 답변에 체크 됐는지 알 수가 없는 상황이다... 그래서 찾아봐야한다. 


32. 웹페이지가 마운트 될때마다 API를 매번 찌르니 너무 느린 것 같다...
그래서 react-query를 쓰는 건가?? 
어떻게 해결해야하지? 



웹페이지 마운트 언마운드 업데이트 다시 정리 관련 : [[usages of useEffect]]


33 TypeError: Cannot read properties of undefined (reading 'protocol')


34.form 데이터에 tyPe을 넣지 못해서 고객페이지에서 받았을떄 타입을 모르니 보여지지가 않는다. 

어떻게 하면 좋을까
공식문서

Input의 타입을 radio로 하고 클릭하면 타입이 들어가긴하는데 이건 아닌 것 같다
![[스크린샷 2022-10-06 오후 3.05.21.png]]

![[스크린샷 2022-10-06 오후 3.17.02.png]]

타입을 넘버로 줬고 벨류는 인덱스값을 주고 disabled로 하니 데이터가 넘어간다. ![[스크린샷 2022-10-06 오후 3.29.08.png]]
tel로 해줬다

옵션에 빈 애가 있다? 그럼 이렇게 보이는 문제

![[스크린샷 2022-10-06 오후 4.06.56.png]]

이미지를 보내면 타입이 1번이 된다.

![[스크린샷 2022-10-06 오후 4.40.19.png]]

아니다...생각이 짧음!! type에 인덱스가 들어가게 된다.

다시!!

35. 상황
form Provider를 surveyEditor에 감싸고 있어서 EditorModal을 surveyEditor 안에서만 보여줄 수 있어서 이렇게 하는 것 같아서 수정해보려고 한다.
![[스크린샷 2022-10-06 오후 6.17.48.png]]![[스크린샷 2022-10-06 오후 6.33.43.png]]
formProvider을 최상단으로 감싸주고 form의 위치를 바꾸니 어렵지 않게 해결 했다. 

36. 메인 페이지에서만 네브가 보였으면 좋겠다.
![[스크린샷 2022-10-06 오후 7.11.10.png]]

이렇게 놓고 Outlet함수를 사용하니
출처 : https://youtu.be/CHHXeHVK-8U



37. useFormContext를 사용하는데 recoil을 사용할 필요가 있나?? 라는 망고님의 질문에 대한 생각 정리해보기 그리고 적용할 수 있으면 적용해보기 

[[Context API]] 기반으로 만들어진 formContext


38. 에러 메세지 오류 이걸로 해결해볼까?
![[스크린샷 2022-10-07 오전 8.46.19.png]]



39. 에러가 없어도 스타일은 보여진다? 그래서 ErrorMessage라는 컴포넌트를 사용해보려고 한다, ![[스크린샷 2022-10-06 오후 6.17.48.png]]
해결!! ![[스크린샷 2022-10-07 오전 8.55.30.png]]

# 41. 관리자 설정하러 가기 버튼을 눌렀을떄 유효성검사가 이루어지고 싶은데... 에러 객체가 생기는 시점이 폼이 생성되는 시점이다.. 그래서 관리자 설정에 들어가서 완료 버튼을 누를때 실행이 되는 문제가 있어서

관리자 설정하러가기 할때 button에 type=input을 줘서 이때 폼을 날아가게 해야하나? 라고 생각했느데 그럼 백앤드 서버로 두번의 데이터가 넘어가게 되어 비효율적이라고 판단했다.

그럼 수동적으로 할 수 있는게 없을까?  하다가 찾게 된 것 react-hook-form의 trigger

![[스크린샷 2022-10-07 오전 9.06.34.png]]


# 42. 다음으로 가기를 클릭했을때 trigger가 발동되는데 그때 errors 객체가 True면 모달이 나오지 않도록 하고 싶다. 

> 모든 문제는 트리거가 됐을떄 errors 객체에 담겨서 한번 늦게 실행한다는 문제에서 시작!!


-> 비동기로 처리해야할 것 같다 그래야 문제없이 실행될 것 같다.
![[스크린샷 2022-10-07 오전 10.25.57.png]]
  
문제 상황  
onClickHandler 함수 안에 있는 Trigger 함수는 세가지 유효성 검사를 수동으로 진행시켜 유효하지 않으면 이 함수 밖에 있는 errors 객체에 각 객체를 추가시킨다.그런데 onClickHandler가 실행될 당시 Errors는 빈객체여서 아래에 있는 기능이!! 무효한 상황

클릭하면 OnClick 함수 실행 -> trigger 함수 발동 4가지 에러 수동으로 실행 -> 전역에 있는 error 객체에 담긴다. -> error를 본다 -> 당연히 없지  

1. 클릭 이벤트에 거는 것이 아니라? 다른 방법으로 할 수 있는 방법이 있을까?
2. 클릭 이벤트가 발생하는 동시에 error 객체에 담길 수 있으면 어떨까?

클릭했을때 에러에 담기게 하면 안된다? 그럼 그 시점을 어떻게 조절해야하는 거지?  그럼 언제 해야하는거지?

-> onClick에서 한단계 나눠주면 안되나?

**true and false를 써서 값이 트루면 onClickTrigger 함수를 할 수 있게 하면 어떨까**

```js
<Button
	type="button"
	onClick={async () => {
		const result = await trigger([
		'surveyName',
		'startDate',
		'endDate',
		])
	if (result) {
		onClickTrigger(errors)
	}
	}}
>
```

시점을 나눠주니 해결 




# 43. 최종 QA때 발견한 에러
1. 폼을 삭제했는데... 삭제한 form이 고객 페이지에서는 보여진다.
	2. 유효성 검사 다시 체크 하기 
		1. 제목
		2. 날짜 (4 - 2-2) 
		3. 폼데이터가 없으면 
	3. 사소한 css 
	4.  고개페이지에서 완료 눌렀을때 랜딩 페이지로 이동 시키는 것. 
	5. 에디터 설정 완료 후, 받은 링크!! 우리 링크로 받아야한다. 
	6. 통계 헤더 필요하다. 


## 설문지 생성 페이지
### 질문 항목 중 삭제를 한 경우, 보여지는 UI에서는 삭제가 됐지만 서버로 보내지는 데이터에선 삭제가 반영이 되지 않는 상황 

#### 현재 UI는 state 객체를 렌더링한다.
1. 선택항목을 누르면 State 객체에 해당 항목에 관련한 데이터가 추가된다.
2. 선택항목에 대한 컴포넌트가 실제 렌더링 되기 전, react-hook-form의 register를 통해 해당 input의 ref를 저정하고 이 값은 useForm 내부 값으로 저장 된다.
3. 생성된 항목을 삭제하면 State 객체에 데이터의 해당 ID를 삭제한다. 
-> 당연히 삭제가 되지 않는다. 삭제하는 로직이 없다.

그렇다면 삭제하는 로직을 추가하는게 맞는건가? 

여기서 근본적인 문제는 하나의 UI를 표현하는데 두개의 값을 사용한것. 

해결 방법 
1. unregister 로직을 삭제시 추가한다. 
```js
import React, { useEffect } from "react";
import { useForm } from "react-hook-form";

export default function App() { 

const { register, handleSubmit, unregister } = useForm()

	useEffect(() => { 
		register("lastName");
		}, [register]) 
	
	return ( 
	<form>
	  <button type="button"
	   onClick={() => unregister("lastName")}>unregister</button>
	   <input type="submit" /> </form> )
	   ; }
```

근본적인 해결 방법
1. 근본적인 문제는 UI에 해당하는 값이 두개라는 것이 핵심이라고 판단했다. 첫번째는 선택항목을 눌렀을때 state에 선택항목에 해당하는 데이터를 추가하고 해당 하는 항목 컴포넌트가 UI에 마운트 될때 input에 react-hook-form의 register를 활용하여 또 다른 상태의 값을 만들었던 것. 기존의 FormList라는 state를 제거하고 useFormContext라는 react-hook-form 라이브러리에서 제공해주는 Context를 사용하여 선택항목이 클릭될때 해당 선택 항목 컴포넌트가 마운트되어 ref에 있는 값을 다른 컴포넌트에서 get하여 보여주는 로직으로 수정.


### 언제 추가 되는지 봐야할 수 있겠따. 
아무것도 없을때 
formList 는 array[0]
만들어진 데이터는 아예 formData가 없음.

option 박스 클릭해서 register코드가 생기면 추가 되는 것 같다. 

register코드가 없어진다고 삭제되는 것 같진 않다. 

핵심 골자 확인
-> GlobalQuestion의 onclick시에 unregister을 해주면 될 것 같다. 

![[스크린샷 2022-10-08 오후 12.22.44.png]]
삭제하는 함수에 각 id의 -1 번쨰의 폼데이터를 삭제하라!! 라는 코드로 도전
-> 모든 폼 리스트 중 마지막을 눌렀을떄만 실행이된다. 

5개 중 2번째를 누르면 안됨.

unregister을 버튼에 거는게 맞나 싶다...

왜냐하면 하나일때는 삭제가 되는데??? 2, 3개일때는 안되는 상황. 

앞에 있는 것을 지우면 뒤에 있는 것이 앞으로 오고 뒤에있던 것이 가만히 있는 상황 


`unregister(`formData[${sortIndex - 1}]`);```

123457 에서 3을 지웠을떄 
4가 3이 되고 

![[스크린샷 2022-10-08 오후 1.16.04.png]]

해당 하는것이 사라지고 다시 자리를 찾아서 2가 1이 된 후 푸쉬하니깐 이러는 것 같다.

그럼 어떻게? 푸쉬할때 해주면 안되나? 

#### 삭제가 되는 과정 생각 
모든 데이터를 포함하고 formList.formData.filter해서 form .id와 눌려진 id와 같지 않은 것을 반환하도록 만들었는데

unregister은 어떻게 해야하는 것 일까? 

현재 문제
3개의 객체가 있고 첫번째 객체를 삭제하면 ui적으로 삭제가 되는 동시에 2번 3번이 각각 1번 2번으로 오게 된다. 그래서 원래 있던 1번이 사라지고 새로 생긴 1번 2번이 오면 되는 것 맞는 것 같은데...

해당하는 것과 마지막에 있는 애를 삭제해주면서 가깝게 왔지만... 완벽하지 않은 논리이다. 
![[스크린샷 2022-10-08 오후 2.00.01.png]]

# 52. 보여지는 formList에서는 삭제되는데 정작 보내지는 formData에서는 삭제가 안되는 문제 

## 생각의 흐름
1. 몇 번이 클릭 됐는지를 배열에 담고
```jsx
setClickedId(prev => [...prev, id]);
```

2. 이것을 리코일 저장소에 담아 해당 컴포넌트에서 불러와서 

3. 클릭된 애들을 맵돌려서 register된 애들을 없애줘야하는데
``` jsx
clickedId.map(el => {return unregister(`formData[${el - 1}]`);});
```


이렇게 하려고 했는데... 결국 실패!!!! 잠시 내려놓음

**해결 출처** : https://www.youtube.com/watch?v=TM99g_NW5Gk


==shouldUnregister: true를 붙혀주니깐 됐다!!! 어렵게 하려고 했는데 useForm 안에서 내장 함수가 있었다.==


# 53. 삭제했을떄 벨류가 그 전 벨류로 이어지는 에러 ![[화면 기록 2022-10-10 오후 4.41.16.mov]]
46 데이터를 받아와서 고객페이지를 보여줄때 만난 에러 
property undefined
![[스크린샷 2022-10-10 오후 5.59.24.png]]

쓸데없는 axios가 하나 덩그러니 있었다... 이게 undefined!! 
![[스크린샷 2022-10-10 오후 6.16.27.png]]

48. 왜 두개가 삭제되는건가요? 
![[스크린샷 2022-10-10 오후 7.02.47.png]]

![[스크린샷 2022-10-10 오후 7.24.32.png]]
저 코드 주석으로 처리하니깐 해결! 

왜 아이디 값이 똑같은게 있지? 
클릭했을떄 아이디 값이 갱신되는게 정상인ㄷ 

49. 이미지를 저장하고 이미지 위에 질문을 삭제하면 이미지 저장된 정보가 사라진다. 
왜??????


50. 베포한 이후에 복사가 안됨.

![[스크린샷 2022-10-11 오전 10.50.43.png]]

하지만 내 localhost에서는 잘 되는 에러!! 
과연 뭐가 문제일까?

-> 

# 51. 배열에서 filter하면 empty가 생기는데 이부분 에러 해결
출처 : https://hianna.tistory.com/423


filter 함수는 값이 할당되지 않은 index는 순회하지 않습니다.

오!! unregister해야하나? 

shouldUnregister로 했는데 안된다.


# 52. The result of getSnapshot should be cached to avoid an infinite loop
lastFormId 변수의 id 앞에 optional chaining을 붙히면 아예 런타임에서 에러가 생김
![[스크린샷 2022-10-12 오후 11.07.28.png]]