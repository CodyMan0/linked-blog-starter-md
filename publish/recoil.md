참고 자료 : https://tech.osci.kr/2022/06/16/recoil-state-management-of-react/
참고 자료 : https://abangpa1ace.tistory.com/212

참고 : [[MVC pattern]] -> [[Flux pattern]] 

- 리코일 핵심은 상태 관리 


## recoil이 자신을 소개하는 문구
1. 작고 react 스러운
2. 데이터 흐름 그래프
3. 교차하는 앱 관찰

## 핵심 개념
### atom
### selector
정의 : selector 은 atom 을 활용해 개발자가 원하는 대로 값을 뽑아서 사용할 수 있는 API 입니다
특징 : 
1. selector 은 readonly 한 값 만을 반환
2. get과 set이 있다.

장점 : [[caching]] -> selector 을 활용해 비동기 통신을 하였을 때 체감되는 강력한 기능은 **캐싱** 입니다. selector 을 활용해 비동기 통신을 해온다면, 내부적으로 알아서 값을 캐싱 해주기 때문에 이미 한번 비동기 통신을 하여 값이 캐싱되어 있다면 매번 같은 비동기 통신을 하지 않고 캐싱 된 값을 추적하여 사용합니다.

#### 관련있는 메모
[[SQL]]의 select ??




### 리액트 안에서는 getter 와 setter를 직접 정의해서 쓰는 Selector라는 순수함수가 있다. 
