공식 문서 : https://kit.svelte.dev/docs/introduction

[[svelte working process]]
## 주제 : svelte
브라우저에 실행될떄 하는 모든 과정을 사이트가 배포 되기 전에 미리 다 해둠.  
Svelte 주의 : 탄생한지 별로 안됐기 때문에 기능이나 커뮤니티가 덜 쌓인 부분들이 있다.

## Svelte란
리액트와 뷰와 다르게 프레임워크 혹은 라이브러리가 아니다? 컴파일러에 가깝다? 

스밸트가 JS 코드로 브라우저가 이해할 수 있도록 컴파일을 해준다. 그래서 프레임워크 혹은 라이브러리를 다운로드할 필요가 없다. 


## 사용 방법 
1. script 
2. style
3. HTML 


## 기본적으로 제공해주는 svelte 기능 
1. 유저 인풋과 값을 DOM에 더욱 쉽게 연결
```js
<script>
let name = '';
</script>

<input bind:value={name}>
<h2>hello {name}</h2>
```



# 차이
## 리액트와의 차이 
1. [[virtual-dom]]을 사용하지 않는다. 
-> 그렇다면 변경된 상태를 어떻게 효율적으로 업데이트하는거지? 
-> 컴파일러가 더욱 최적화된 JS코드를 만들어서 빠르게 UI를 업데이트할 수 있도록 한다. 









## 나만의 언어로 정리



### 출처(참고문헌)

### 연결문서
- [[react MOC]]
- [[vue]]
- [[AngluarJs]]
