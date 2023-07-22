
# 웹팩 개념


## 특징 
1.  여러개의 파일을 하나로 묶어주기 때문에 ==네트워크 접속의 부담을 줄 일 수 있습니다==. ==더 빠른 서비스를 제공==할 수 있습니다. 
2.  여러개의 서로 다른 패키지들이 **서로 같은 이름의 전역 변수를 사용하면 프로그램은 오동작**하게 됩니다. 이런 문제를 극복하기 위해서 등장한 것이 ==모듈==입니다. 웹팩은 
3.  **웹팩에는 매우 많은 플러그인**들이 존재합니다. 이런 플러그인을 이용하면 웹개발시에 필요한 다양한 작업을 **자동화** 할 수 있습니다. 

## furtherMore
-   [[loader]]개념
-   [[plugin]] 개념

## 정리
[[Typescript_Moc]]와 사용하면 더 나은 프로젝트 설정이 가능하며, 이 도구를 사용하여 특정 작업을 더 쉽게 하고 두가지의 장점인 높은 개발 경험과 최종 사용자에게 적합한 코드 

## 글감
[[webpack and CRA]]


### 연결 문서
- [[npm]]
- [[Babel]]


## 사용 이유

웹팩을 사용하는 이유 : 

```
//root
- main.js
- run.js
- walk.js
- index.html
```
이라는 js파일이 있다고 생각해보겠습니다. 각각의 JS파일에 맞는 코드가 작성되어있고 index.html에서 body 하단부에 script 태그를 통해서 불러오고 있다고 가정하겠습니다. 이렇게요 

```Html
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="UTF-8" />
		<meta http-equiv="X-UA-Compatible" content="IE=edge" />
		<meta name="viewport" content="width=device-width, initial-scale=1.0" />
		<title>mockHomepage</title>
		<link rel="stylesheet" href="style.css" />
		<link rel="preconnect" href="https://fonts.googleapis.com" />
	</head>
	<body>
		<section id="root">
			<img src="bg.jpg" id="bg" />
			<img src="moon.png" id="moon" />
			<img src="mountain.png" id="mountain" />
			<h2 id="text">it's time to sleep</h2>
		</section>
		<script src="./main.js"></script>
		<script src="./run.js"></script>
		<script src="./walk.js"></script>

//웹펙 사용 후
		<script src=".public/index_bundle.js"></script>
	</body>
</html>

```

웹팩 설정 
```js
var path = require("path");

module.exports = {
	mode: "none",
	entry: "./src/index.js",
	output: {
		filename: "index_bundle.js",
		path: path.resolve(__dirname, "public"),
	},
};

```

live server를 통해서 웹페이지에 접근하고 network panel을 살펴보면 3개의 js파일이 각각 받아와진다는 것을 확인할 수 있습니다.  그렇다면 여기서 수 많은 파일이 있다고 가정한다면 웹페이지에 접근했을때 JS파일을 받는데 시간이 과도하게 걸릴 겁니다. 이러한 문제를 해결하기 위해 webpack을 활용하여 js파일을 하나의 js파일로 합쳐줘 여러 방면에서 이점을 주고 있습니다. 하나씩 알아봅시다 .



웹팩을 활용했을때 가장 큰 이점은 모든 JS 파일을 일일이 서버로 부터 다운로드 받지 않고 한번에 모든 자바스크립트 파일을 받아 유저의 사용 경험을 높일 수 있다는 점입니다.



## 설정
### mode 
```js
//mode가 production 일때
//index_bundle.js
(() => {
	"use strict";
	(() => {
		let t = document.getElementById("bg"),
			e = document.getElementById("moon"),
			n = document.getElementById("mountain"),
			o = document.getElementById("road"),
			l = document.getElementById("text");
		window.addEventListener("scroll", function () {
			const d = window.scrollY;
			(t.style.top = 0.5 * d + "px"),
				(e.style.left = 0.5 * -d + "px"),
				(n.style.top = 0.15 * -d + "px"),
				(o.style.top = 0.15 * d + "px"),
				(l.style.top = 1 * d + "px");
		});
	})();
})();


//mode가 development일때 
//index_bundle.js

/******/ (() => { // webpackBootstrap
/******/ 	"use strict";
/******/ 	var __webpack_modules__ = ({

/***/ "./main.js":
/*!*****************!*\
  !*** ./main.js ***!
  \*****************/
/***/ ((__unused_webpack_module, __webpack_exports__, __webpack_require__) => {

eval("__webpack_require__.r(__webpack_exports__);\n/* harmony export */ __webpack_require__.d(__webpack_exports__, {\n/* harmony export */   \"default\": () => (__WEBPACK_DEFAULT_EXPORT__)\n/* harmony export */ });\nconst main = () => {\n\tlet bg = document.getElementById(\"bg\");\n\tlet moon = document.getElementById(\"moon\");\n\tlet mountain = document.getElementById(\"mountain\");\n\tlet road = document.getElementById(\"road\");\n\tlet text = document.getElementById(\"text\");\n\n\tconst effect = function () {\n\t\tconst value = window.scrollY;\n\n\t\tbg.style.top = value * 0.5 + \"px\";\n\t\tmoon.style.left = -value * 0.5 + \"px\";\n\t\tmountain.style.top = -value * 0.15 + \"px\";\n\t\troad.style.top = value * 0.15 + \"px\";\n\t\ttext.style.top = value * 1 + \"px\";\n\t};\n\n\twindow.addEventListener(\"scroll\", effect);\n};\n\n/* harmony default export */ const __WEBPACK_DEFAULT_EXPORT__ = (main);\n\n\n//# sourceURL=webpack://activepage/./main.js?");

/***/ }),

/***/ "./src/index.js":
/*!**********************!*\
  !*** ./src/index.js ***!
  \**********************/
/***/ ((__unused_webpack_module, __webpack_exports__, __webpack_require__) => {

eval("__webpack_require__.r(__webpack_exports__);\n/* harmony import */ var _main_js__WEBPACK_IMPORTED_MODULE_0__ = __webpack_require__(/*! ../main.js */ \"./main.js\");\n\n\n(0,_main_js__WEBPACK_IMPORTED_MODULE_0__[\"default\"])();\n\n\n//# sourceURL=webpack://activepage/./src/index.js?");

/***/ })

/******/ 	});
/************************************************************************/
/******/ 	// The module cache
/******/ 	var __webpack_module_cache__ = {};
/******/ 	
/******/ 	// The require function
/******/ 	function __webpack_require__(moduleId) {
/******/ 		// Check if module is in cache
/******/ 		var cachedModule = __webpack_module_cache__[moduleId];
/******/ 		if (cachedModule !== undefined) {
/******/ 			return cachedModule.exports;
/******/ 		}
/******/ 		// Create a new module (and put it into the cache)
/******/ 		var module = __webpack_module_cache__[moduleId] = {
/******/ 			// no module.id needed
/******/ 			// no module.loaded needed
/******/ 			exports: {}
/******/ 		};
/******/ 	
/******/ 		// Execute the module function
/******/ 		__webpack_modules__[moduleId](module, module.exports, __webpack_require__);
/******/ 	
/******/ 		// Return the exports of the module
/******/ 		return module.exports;
/******/ 	}
/******/ 	
/************************************************************************/
/******/ 	/* webpack/runtime/define property getters */
/******/ 	(() => {
/******/ 		// define getter functions for harmony exports
/******/ 		__webpack_require__.d = (exports, definition) => {
/******/ 			for(var key in definition) {
/******/ 				if(__webpack_require__.o(definition, key) && !__webpack_require__.o(exports, key)) {
/******/ 					Object.defineProperty(exports, key, { enumerable: true, get: definition[key] });
/******/ 				}
/******/ 			}
/******/ 		};
/******/ 	})();
/******/ 	
/******/ 	/* webpack/runtime/hasOwnProperty shorthand */
/******/ 	(() => {
/******/ 		__webpack_require__.o = (obj, prop) => (Object.prototype.hasOwnProperty.call(obj, prop))
/******/ 	})();
/******/ 	
/******/ 	/* webpack/runtime/make namespace object */
/******/ 	(() => {
/******/ 		// define __esModule on exports
/******/ 		__webpack_require__.r = (exports) => {
/******/ 			if(typeof Symbol !== 'undefined' && Symbol.toStringTag) {
/******/ 				Object.defineProperty(exports, Symbol.toStringTag, { value: 'Module' });
/******/ 			}
/******/ 			Object.defineProperty(exports, '__esModule', { value: true });
/******/ 		};
/******/ 	})();
/******/ 	
/************************************************************************/
/******/ 	
/******/ 	// startup
/******/ 	// Load entry module and return exports
/******/ 	// This entry module can't be inlined because the eval devtool is used.
/******/ 	var __webpack_exports__ = __webpack_require__("./src/index.js");
/******/ 	
/******/ })()
;
```

개발 모드보다 production 코드는 불필요하게 긴 변수명까지 축소시켜 가장 경량화시켜 코드를 축소시킵니다. 


### style까지 함께 bundling 

![[스크린샷 2023-03-27 오후 4.23.17.png]]
모든 js파일을 하나로 뭉쳤는데 css도 당연히 합칠 수 있지 않을까!! 

어떻게? **loader**

터미널로 설치 
> npm install -D style-loader css-loader


```js
//webpack.config.js
var path = require("path");

module.exports = {
	mode: "development",
	entry: "./src/index.js",
	output: {
		filename: "index_bundle.js",
		path: path.resolve(__dirname, "public"),
	},
	module: {
		rules: [{ test: /\.css$/, use: ["style-loader", "css-loader"] }],
	},
	//style-loader를 통해서 자동적으로 style이 삽입된 것을 볼 수 있습니다. 
};

```


![[스크린샷 2023-03-27 오후 4.34.30.png]]

.css 파일이 발견되면 use가 실행되는 것. 여기서 주의할 것은 배열의 뒷 인덱스 부터 실행됩니다. 그렇다면 css-loader가 먼저 실행되겠죠? 그 다음 style-loader가 실행된다. 

반대로 실행하면 에러 
>  /Users/leejuyoung/Documents/projects/dev/homePages/activePage/src/style.css Unknown word

css 파일을 찾을 수가 없다고 합니다. 


## 주요 용어

**주요 용어**

**설명**

**Entry**

- 번들링을 시작하기 위한 최초 진입점의 자바스크립트 파일 경로를 설정하는 옵션입니다.

**Output**

- Entry에서 지정한 진입점을 바탕으로 결과물(Bundle)을 반환하는 설정을 하는 옵션입니다.

**Loader**

- 자바스크립트 파일 외에 다른 포맷(HTML, CSS, Image, Font 등..)의 파일을 처리하여 앱에서 사용 할 수 있도록 모듈로 변환 할 수 있도록 도와주는 옵션입니다.

**Plugins**

- Webpack의 기본적인 동작에 추가적인 기능을 제공하는 옵션입니다.

**Resolve**

- Webpack에 기본값을 제공하지만 상세하게 해석 방식을 변경에 대한 설정을 하는 옵션입니다.

**Mode**

- Webpack에 내장된 최적화 기능을 사용할 수 있는 옵션입니다.
## 웹펙이는 두가지 확장 기능 
1. 로더 -> 모듈들을 최종 아웃풋으로 만들어가는 과정에서 사용되는 것이 로더 
2. 플러그인  -> 만들어진 결과물을 변형할 수 있게 해주는 것이 플러그인 


### 플러그인 



## 이렇게 웹펙을 사용해서 하나의 파일로 만들었는데 크기가 크다면? 

웹팩에서 제공하는것 -> [[code splitting]] 그리고 [[lazy loading]]을 생각해볼 수 있습니다. 



# 리액트에서 웹팩이 어떻게 녹아들어있나? 
```
npx create-react-app 파일 이름 
```

설치가 완료된 후 해당 디렉토리로 들어가 VScode를 실행시켜준 후 설정파일을 보이도록 합니다.
```
npm run eject
```
npm run ejecct로 명령어로 설정파일을 볼 수 있게 됩니다. 지금까지 react를 사용하고 있었으나 이렇게 자세하게 설정을 본 것은 창피하지만 처음입니다. 미친 추상화... 


오호라 `config` 와 `scripts` 폴더가 생겼습니다.


참고 자료 : https://berkbach.com/create-react-app-%EC%9D%98-webpack-config-js-%EB%93%A4%EC%97%AC%EB%8B%A4%EB%B3%B4%EA%B8%B0-78e40bf37313


# vite와 webpack을 활용하여 만들어진 CRA 전격 비교

EsBuild는 Go와 같은 low-level language를 활용하여 생겨난 자바스크립트 툴 
vite는 Esbuild를 기반으로 만들어진 프론트엔드 빌드 툴 

# 관계도 


