


CSR과 SSR 글과 Critical Rendering path에 대해 글을 쓰면서 정리했지만 [[Single Page Application]]은 **[[MPA]](Multi Page Application)의 문제점**을 해결하기 위해서 나오게 된 해결 방법이다. MPA의 문제점은 페이지 이동에 따라 HTML 전체를 새롭게 가져와야 하는 불필요한 비용이 발생한다는 점!

이를 해결하기 위해 하나의 html에 javascript을 이용해 동적으로 DOM요소를 변형하는 `SPA (Single Page Application) 방식`이 제안되었고 여기에 대표적인 라이브러리가 바로 **리액트**이다.

하지만 SPA는 DOM요소를 자바스크립트로 직접 건드리기 때문에 Critical Rendering Path에서 브라우저가 그려줘야하는`layout -paint- composite`과정이 다시 일어나야 해서 성능이 큰 문제가 될 수 있다. 이러한 성능 문제를 해결하기 위해서 리액트는 자체적인 V-DOM을 이용한 Reconcilation으로 해결한다. 두가지에 대해서 알아보자.




### 관련있는 메모
1. [[CSR and SSR]]