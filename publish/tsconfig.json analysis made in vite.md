
typescript가 어떻게 컴파일할지 설정하는 파일이 tsconfig.json! 

![[스크린샷 2022-12-06 오후 3.28.01.png|500]]
** 기본 프로젝트에서 tsc --init 을 하면 모든 설정들에 대한 주석을 볼 수 있다. 

1. exclude :는 tsc가 실행될때 포함지 않았으면 하는 파일을 말한다. 
	exclude를 작성하지 않으면 자동적으로 node_module이 제외된다 ,
	include는 반대 "src" 파일에 포함되는 것만 컴파일 하겠다는 것. 그 외에 아무것도 컴파일 하지 않는다. 

2. compilerOptions : 타입스크립트 코드가 컴파일되는 방식을 관리하는 객체
	1. target option :  어떤 자바스크립트 버전으로 컴파일 할것인지 
		Q. 엇 그럼 바벨의 역할을 타입스크립트 설정으로 대체할 수 있는것 같다?? 
		> 바벨 : 자바스크립트의 [[컴파일러]]로 [[cross-browsing issue|크로스브라우징]] 이슈를 해결하기 위해 최신 Es 버전의 자바스크립트 코드를 구 버전으로 바꿔주는 역할

	어느정도 IE 호환성을 원하시면 es5, commonjs가 국룰임
		정리해보면 'ESNest' 는 
		The special ESNext value refers to **the highest version your version of TypeScript supports**.
		
	2. lib은 Dom으로 작업을 수행하는 항목들이 적혀있다. 
		"lib" : ["DOM"]
		-> 타입스크립트가 이해할 수 있는 DOM API를 제공해준다!!!!
		"lib" : ["DOM.Iterable"]
		-> iteration 문법을 타입스크립트가 이해할 수 있도록 제공해준다.
		여기서 #Q.DOM에 iteration이 포함되어있는거 아닌가????
		
		I suspect it's because iteration (iterables and iterators) **weren't added to JavaScript until ES2015**, long after TypeScript was well-established. When ES2015 was released, the JavaScript engines in many browsers didn't support iteration (yet),¹ and of course at the time Internet Explorer was still a...thing...that was never going to get new features. So some projects had to target environments that didn't have iteration, so the libs are separate.

		Even here in 2022, IE survives in corporate and government installations (although thankfully that's _finally_ changing), and some folks have to target their apps and pages to those environments, so they wouldn't want to use `dom.iterable`.
		
		"lib" : ["ESNext"]
		-> 타입스크립트가 ESNext 문법을 인지할 수 있도록 해준다. 


	3. 

![[스크린샷 2022-12-06 오후 3.28.01.png|500]]
4. [https://www.typescriptlang.org/tsconfig#strict](https://www.typescriptlang.org/tsconfig#strict)
5. 