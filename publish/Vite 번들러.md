출처 : https://ko.vitejs.dev/guide/

# 핵심 

- Go로 만든 bundler 라이브러리인 esBuild로 빌드를 진행  (webpack5보다 빠르다)

- npm package 이용한 웹 개발시, 의존성 있는 패키지 소스코드를 esbuild를 사용하여 빠르게 pre-bundling 해주고 es6 모듈 문법과 HMR을 이용해 실시간 미리보기 기능도 제공해주고 jsx와 css module 번들링도 알아서 잘 되는 번들링 툴.


## 특징
1. 빠른 개발 서버 시작
	### how? 
	![[스크린샷 2023-07-11 오후 4.57.16.png]]
	기존에는 개발서버가 켜지는 원리는 이러하다.
	 베포시 dist (베포 Output 풀더라고 가정)폴더에 파일을 브라우저에 온전히 로드해야했다.  왜냐하면 리액트같은 경우 jsx 문법은 브라우저가 알 방법이 없기 때문이다. 즉 트랜스 파일링을 거쳐서 보여줘야했다. 그러다보니 프로젝트가 커지면 커질수록 느려질 수 밖에 없었다.

	하지만 vite같은 경우는 
	![[스크린샷 2023-07-11 오후 4.57.33.png]]
	예를 들어 /http://localhost:5173/project로 들어가는 순간 해당 라우트에 필요한 것들만 추려서 실시간으로 serving을 해준다. 그로 인해 빠르게 실행할 수 있게 됐다는 의미이다. 

**실제로 프로젝트를 통해 확인해보았다.**

하지만 여기서 발견한 것은
현재 진행중인 프로젝트를 통해 확인해본 결과, 메인 페이지 마운트시 메인 페이지에서 사용되지 않는 모듈도 함께 로드가 되는 상황이었다. 
![[스크린샷 2023-07-11 오후 5.01.36.png]]
Q. 블로그를 통해 정리한 바로는 해당 페이지가 마운트될때 필요한 것만 로드된다고 하는데 프로젝트 메인 페이지가 마운트됐을 경우는 모든 js 파일을 다 로드하고 있다. 왜 그러는지 아실까요?

A. ??



2. vite는  esbuild를 사용해서 app의 디팬던시를 pre-bundle한다. JS기반 번들러보다 훨씬 빠르고 그로 인해 개발 중에 불필요한 작업을 하지 않게 되거 더 나아가 앱을 렌더링하기 까지 걸리는 로딩 타임을 줄일 수 있게 됐다. 

3. vite는 빠른것 뿐 아니라 다양한 기능도 있고 확장이 가능하다. 프론트엔드의 대부분의 라이브러리에서 호환이 가능하며 기본 설정을 제공하여 개발자로 하여금 쉽게 사용할 수 있게 한다. 

4. 프로덕트를 빌드할때면, tree-shacking과 code-splitting을 최적화한 Rollup을 번들러 내부에서 사용하고 있다. 최소화, 해싱, 압축, 브로틀리 압축과 같은 다양한 최적화를 적용한다고 한다. 개발자는 공부하지 않으면 모르고 쓰기 쉽상이다. 

## 간단히 build.minify 살펴보기 

```ts
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'

// https://vitejs.dev/config/
export default defineConfig({
  plugins: [react()],
})
```

plugins라는 객체의 프로퍼티에 배열 안에 react()가 있다. 

현재 프로젝트에서 build한 결과물을 살펴보면
```bash
➜  aligo-oligo-latest git:(develop) npm run build

> aligo-oligo-latest@0.0.0 build
> tsc && vite build

vite v4.3.9 building for production...
✓ 510 modules transformed.
dist/index.html                     2.62 kB │ gzip:   2.03 kB
dist/assets/logo-e2c26e93.png      13.60 kB
dist/assets/oliBody-9d3c2b45.png   22.27 kB
dist/assets/hero-ea6163dd.jpeg     72.34 kB
dist/assets/index-e78a994b.css     39.51 kB │ gzip:   7.14 kB
dist/assets/index-54d2d32d.js     598.24 kB │ gzip: 181.15 kB

(!) Some chunks are larger than 500 kBs after minification. Consider:
- Using dynamic import() to code-split the application
- Use build.rollupOptions.output.manualChunks to improve chunking: https://rollupjs.org/configuration-options/#output-manualchunks
- Adjust chunk size limit for this warning via build.chunkSizeWarningLimit.
✓ built in 7.01s
```

한달간 진행된 프로젝트여서 사이즈가 큰데도 불구하고 7초의 빌드시간과 최적화 가이드 라인을 제공 

**assets/index-54d2d32d.js**
![[스크린샷 2023-07-11 오후 4.41.12.png]]

```ts
export default defineConfig({
	plugins: [react()],
	build: {
		minify: false,
	},
});

```
위와 같이 config 파일을 수정하니 아래와 같이 보여지게 됐다. 하지만 bundle 사이즈가 당연히 커졌다. 
![[스크린샷 2023-07-11 오후 4.44.00.png]]

알아볼 수 있으며 ,

빌드 시간은 7초에서 약 9초로 2초 증가, 파일 크기는 약 2배가량 차이난다.

```sh
// minify : true (default)
dist/index.html                     2.62 kB │ gzip:   2.03 kB
dist/assets/logo-e2c26e93.png      13.60 kB
dist/assets/oliBody-9d3c2b45.png   22.27 kB
dist/assets/hero-ea6163dd.jpeg     72.34 kB
dist/assets/index-e78a994b.css     39.51 kB │ gzip:   7.14 kB
dist/assets/index-54d2d32d.js     598.24 kB │ gzip: 181.15 kB


// minify : false 
dist/index.html                       2.62 kB │ gzip:   2.03 kB
dist/assets/logo-e2c26e93.png        13.60 kB
dist/assets/oliBody-9d3c2b45.png     22.27 kB
dist/assets/hero-ea6163dd.jpeg       72.34 kB
dist/assets/index-423ad145.css       48.87 kB │ gzip:   9.32 kB
dist/assets/index-6b093028.js     1,131.97 kB │ gzip: 245.34 kB
```

모든 번들러의 기본은 minify 된다. 

Q. 혹시 다른 번들러에서 경험하신것들이 있으신지? 궁금합니다.


### 관련있는 메모
1. [[npm]]과 뗄레야 뗄수 없는 번들러
2. [[webpack and CRA]]
3. [[Turbopack]]
