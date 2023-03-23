### Styles 부분의 순서가 의미하는 것은?

-   하나의 요소에 여러개의 css 파일에서 스타일 적용 가능
-   가장 상단부터 css 파일의 _**우선 순위(구체적 >>> 추상적)**_ 에 따른 순서
-   cf) **`CSS Specificity`** - inline style > id > class > tag

	### `user agent stylesheet` 란?

-   브라우저의 기본 스타일 값을 의미. 브라우저 마다 스타일 기본값이 다름.
-   Chrome, Safari, IE 등 브라우저의 종류에 따라 기본적으로 설정되어 있는 속성 값이 다르기 때문에 개발 시작 단계에서 `reset.css` 혹은 `normalize.css` 파일에서 기본 스타일 값을 모두 초기화 시키고 작업 시작. >>> 브라우저의 종류에 상관 없이 동일한 화면 출력 가능

