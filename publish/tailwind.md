[공식 문서](https://tailwindcss.com/)

# PostCSS인 tailwind

## 정의
Tailwind CSS는 **Utility-First 컨셉**(이름을 지정하지 않고 지정된 CSS클래스를 사용하는 것을 말합니다.)을 가진 CSS 프레임워크입니다.  부트스트랩과 비슷하게 m-1, flex와 같이 미리 세팅된 유틸리티 클래스를 활용하는 방식으로 HTML 코드 내에서 스타일링을 할 수 있게 해줍니다. 

## 등장 배경
과거의 사용해던 styled-component를 살펴보면 스타일 하나하나에 이름을 지정하고  재사용했습니다. 하지만 프로그램이 커지다보면 이름들이 겹치게 돼, **혼동을 야기**하는 경우가 있었습니다. 그래서 등장한게 클래스로 미리 지정해두고 사용할때는 HTML element에 class 안에서 사용할 수 있도록 합니다. 

## 특징
-   Reset.css가 기본으로 탑재(어떤 브라우져서든 동일한 결과를 내도록 CSS 초기화)
-> 부연설명 : 기본 css로 진행할 경우 브라우저 마다 동일한 스타일을 적용시키기 위해 reset.css를 만들어줍니다. 하지만 tailwind를 사용할 경우 기본적으로 내제되어 편리하게 사용할 수 있습니다.

-   Production에는 실제로 사용하는 css만 포함되어 작은 css파일을 유지 가능.
-   shadow, round, space 등 꽤 긴 style을 짧게 표현 가능하여 생산성이 높음.
-   responsive 스타일 적용하기 쉬움
-   hover, focus 등 손 쉽게 처리 가능
- 기본적인 animation 가능을 쉽게 처리 가능 

## (personal) 사용 방법
1. tailwind.css를 사용하고자 하는 라이브러리(react) 혹은 프레임워크(Next.js or svelteKit we use)을 설치합니다.
2. 사용하고자 툴에서 tailwind.css 설치 방법을 찾으면 친절히 알려줍니다. (궁금한 것 있으면 언제든 물어봐주세요)
3. 공식 문서 탭을 띄어놓고 기존에 css를 어떻게 tailwind.css에서 사용할 수 있는지 찾아가며 적용합니다. (처음에 learning curve가 있습니다.)


## 유튜브 강의
1. 코딩 애플 : https://www.youtube.com/watch?v=--D4WMPEIZI
2. 제주코딩 베이스 캠프 : https://www.youtube.com/watch?v=EoDYYPUooKY
3. 유명 강의 : https://www.youtube.com/watch?v=tk11Rl7lyRQ