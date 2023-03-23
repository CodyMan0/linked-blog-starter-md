
### 문제 : 10kb 이상 되는 Record는 업데이트 불가 

#### 원하는 상황 : 수많은 md 파일이 algolia의 index에 추가되면 좋겠는데...

10kb 이상 되는 파일이면 에러 
![](https://velog.velcdn.com/images/sharphand1/post/52971534-1c18-4f8f-b7e7-4b2706fa79c8/image.png)

공식 문서와 커뮤니티를 찾아보고 구글에 
> One of my records is too big. What can I do? 

검색을 해보니


If you get an error about one of your records being too big, **be sure to update the plugin to the latest version.** We keep improving the plugin with ways of making the records smaller.

If you’re still having an error, you should check the .json log file that has been created in your source directory. This will contain the content of the record that has been rejected. It might give you hints about what went wrong.

A common cause for this issue often lies in the page HTML. **Maybe the HTML is malformed **(a tag is not closed for example), or instead of several small paragraphs there is only one large paragraph. This can cause the parser to take the whole page content (instead of small chunks of it) to create the records.

-> 최신 버전으로 업그레이드를 하거나 html의 문제라고 하는데 두가지 모두 진행했으나 여전히 record가 초과했다고 나옵니다. 그래서 단순하게 연관성 그래프를 잠시 삭제해보았습니다. 

그래프 뷰 때문에 record의 용량이 초과되는 것 같습니다. 

![](https://velog.velcdn.com/images/sharphand1/post/aa1806a4-f4d2-484e-b407-9c301eecff47/image.png)



1. 최신 버전으로 업데이트 - [ x ]
2. 완전히 layout에서 지웠는데 왜 여전히 backlinks가 15.19kb일까?
3. hook을 사용해볼까? 공식문서에서 발견 
4. 결국 로그에서 알려준 방식으로 가보자 
	1. 이 문제는 잘못된 형식의 HTML로 인해 파서가 올바르게 작동하지 않은 수 있다는 것.
	2. 편집을 통해 이 오류를 생성하는 페이지를 인덱싱에서 제외 'file_to_exlude'
5. _config.yml에 추가하기 
```
algolia:
  application_id: "VZVRIKH0WD"
  index_name: "digitalGarden"
**  indexing_batch_size: 500
  extensions_to_index:
    - html
    - md
**
```
하지만 모두 실패했습니다. 
6. 마지막으로 jekyll backlinks를 만드는 plugin 깊숙히 들어가 찾아서 해당 backlinks를 만드는 코드를 삭제해주어 해결했습니다. 


## advance 적용 과정

### 문제 : 모든 페이지에 적용되는 문제 

#### 원하는 상황 : note에만 검색창 사용 가능하도록

시도 
1. 어제 작성한 코드는 가장 최상위인 default.html에 작성했습니다. default.html에 있는 script들을 _include/algolia.html에 이동시켜보려고 합니다.

includes / algolia.html을 만들었습니다.
```
<script
	src="https://cdn.jsdelivr.net/npm/algoliasearch@4.14.3/dist/algoliasearch-lite.umd.js"
	integrity="sha256-dyJcbGuYfdzNfifkHxYVd/rzeR6SLLcDFYEidcybldM="
	crossorigin="anonymous"
></script>
<script
	src="https://cdn.jsdelivr.net/npm/instantsearch.js@4.49.4/dist/instantsearch.production.min.js"
	integrity="sha256-Ps194FVLiZAj7tXnC/xW7piaYV5EaKB8NWYu1xAN3Rc="
	crossorigin="anonymous"
></script>
<link
	rel="stylesheet"
	href="https://cdn.jsdelivr.net/npm/instantsearch.css@8.0.0/themes/satellite-min.css"
	integrity="sha256-p/rGN4RGy6EDumyxF9t7LKxWGg6/MZfGhJM/asKkqvA="
	crossorigin="anonymous"
/>

// 위의 두개의 script와 한개의 link를 통해 algolia를 사용할 수 있습니다. 

<script>
	let searchClient = algoliasearch(
		"VZVRIKH0WD",
		"7632330f98e4bfa8d2731641cc0ff3a2"
	);


	const hitTemplate = function (hit) {
		console.log("hit", hit);
		return;
		`<div class="post-item ${additionalClass}">
        <a href=${hit.url}>${hit.title}</a>
      </div>`;
	};
	const search = instantsearch({
		indexName: "digitalGarden",
		searchClient,

	});

	search.addWidgets([
		instantsearch.widgets.searchBox({
			container: "#searchbox",
			placeholder: "Search what you wanna know",
			autofocus: false,
			poweredBy: true,
		}),

		instantsearch.widgets.hits({
			container: "#hits",
			hitsPerPage: 10,
			templates: {
				item: hitTemplate,
			},
		}),
	]);

	search.start();
</script>

```

그리고 UI를 보여주고자 하는 페이지 html로 이동하였습니다.
전 note 관련된 페이지에서만 검색기능을 보여주고 싶기때문에 note.html로 이동하였습니다.

_layouts / note.html
```

	{% include algolia.html %} //liquid 문법을 활용해서 html을 불러옵니다

	<div id="notes-entry-container">
		<content> {{ content }} </content>
		<side style="font-size: 0.9em">
			<h3 style="margin-bottom: 1em">Search knowledge</h3>
			<div id="searchbox"></div>
			<div id="hits"></div> 
```

algolia.html을 liquid 문법을 활용해서 가지고 오고 원하는 위치에 id가 searchbox와 hits를 가진 div를 만들어줍니다. 

**여기서 만난 에러 **
생각보다 얽혀있는 script의 위치때문에 햇갈리기 시작했습니다. 

error : Container must be `string` or `HTMLElement`. Unable to find #searchbox


```

	<div id="notes-entry-container">
		<content> {{ content }} </content>
		<side style="font-size: 0.9em">
			<h3 style="margin-bottom: 1em">Search knowledge</h3>
			<div id="searchbox"></div>
			<div id="hits"></div> 
            
	{% include algolia.html %} //liquid 문법을 활용해서 html을 불러옵니다

```
태그 뒤로 html을 가져와야합니다. 


### 문제 : 입력을 하지 않았는데 결과를 보여주는 문제

#### 원하는 상황 : 입력을 지웠을땐 결과가 없도록 하고 싶습니다.

아무것도 입력하지 않으면 결과물을 보여주면 안되는데 보여주고 있습니다. 찾아보니 searchFunction을 사용하면 검색 행동을 제어할 수 있다고 합니다. 페이지가 로드 됐을때 자동 서치되는 것 방지한다고 합니다. 
![](https://velog.velcdn.com/images/sharphand1/post/95ce918d-9cfe-4930-80e7-3a129289c180/image.png)

searchFunction을 활용하여 적용해봅시다. 

```js
	const search = instantsearch({
		indexName: "digitalGarden",
		searchClient,
	});
```

```js
	const search = instantsearch({
		indexName: "digitalGarden",
		searchClient,
		searchFunction(helper) {
			if (helper.state.query) {
				helper.search();
			}
		},
	});

```
WOW!! 말도 안되게 바로 적용이 됐습니다. searchFunction 매소드를 활용해서 helper라는 매개변수의 query가 true면 hits를 받아오도록 설정하니 해결했습니다. 역시 공식 문서!! 짱짱




### 문제 : 검색 기능을 추가하면 graph를 볼 수 없는 문제
#### 원하는 상황 : 검색과 그래프, 두마리 토끼를 잡고 싶습니다.

현재 상황 : algolia의 record는 하나당 10KB를 넘기면 안됩니다. 하지만 현재 저의 디지털 가든의 하단에 graph를 통해 노트간의 연관성을 보여주고 있습니다. 하나의 노트가 수 십개 혹은 수백개의 노트의 연결성을 확인할 수 있도록 하기 위해서 만든 것인데 연결성을 확인시켜주는 데이터인 backLinks가 노트 안에서 10KB 이상의 데이터를 차지하는 바람에 레코드에 등록하지 못하는 상황이 있었습니다. 그래서 이틀 전, 과감히 backlink generator에 있는 코드를 수정하였습니다. 그 결과 검색 전에는 그래프가 보이지만 검색 후에는 그래프가 보이지 않는 상황이 발생하였습니다. 


**전 **

![](https://velog.velcdn.com/images/sharphand1/post/140cace9-e5dd-47a8-9a68-ae7affe7a32b/image.png)
검색창이 없을땐 문제가 그래프가 보입니다.

후
![](https://velog.velcdn.com/images/sharphand1/post/18e47156-3f5e-4bf6-aba1-72534c571d9e/image.png)

이 문제는 제일 마지막에 다루겠습니다. 
검색 x / 수정 코드 그래프 ->  그래프가 보여진다!! 잘 되는데? 
검색 o / 수정 코드 그래프 -> 그래프가 안보인다. 


script가 읽히는 순서 다시 봐야겠다 

head에 script는 블록 현상
body에 script는 화면은 일직 보여주나 2초정도 검색기능이 안됨. 
head에 script asyn 사용 병렬적으로 다운로드 가능. 사용자가 페이지를 보는데 시간이 걸릴 수 있다.
head 안에서 script defer을 정의하면 parsing하는 동안 script들을 다 받아놓고 parsing이 완료하면 모든 script를 실행하는 방식으로 진행
-> 오호 그럼 head안에서 defer을 넣어볼가? 


그래프만 head안에 넣고 defer 그리고 알골리아는 그대로 

-> 스크립트 위치의 중요성 !! 이제 알았다. 리액트를 사용하면서 import에 익숙해져서 까먹고 있었따. 


알골리아는 head안에 넣고 나머지는 안넣음, -> 문제

음 script의 위치의 문제가 아닌가 싶다. 

그럼 뭐가 문제지? 
검색 o / 원본 코드 그래츠 -> 

도저히 알 수 없다. 이해가 안간다. 

스타일때문도 아니다 aloglia.html style 주석처리하고 보니깐 아니고 

algolia.html 을 주석처리하면 그래프가 나온다. 

검색이 있으면 그래프가 안나온다. 


search funciton문제도 아니고 

-> {% include algolia.html %}

liquid문법을 모르고 사용한 문제같은데 


그래프도 cdn에서 가지고 오고 algolia도 cdn에서 가지고 오는데 여기서 생기는 오류인가? 


그럼 Note에서 include하지 않고 default.html에 옮겨볼까
-> 동일하게 안된다. 뭐가문제지? 

default.html에 있는 link 뭐시리 삭제해봄 
->역시 동일 


-> note_graph.html
window.addEventListener("scroll", loadGraph)로 load -> scroll로 바꿔봄,

-> 오늘은 여기까지 모르겠다 


차이점 
```
const svg = d3.select("svg");
const width = Number(svg.attr("width"));
const height = Number(svg.attr("height"));
console.log(width,height) -->

```

![](https://velog.velcdn.com/images/sharphand1/post/f3d5c943-08b7-445d-84ae-2c239bbb4d54/image.png)

검색창이 있을때는 width :10 height: 10 , svg에 g tag가 생기지 않는다. 하지만 검색창이 없을때는  width: 1200 height: 400 그리고 svg에 g tag가 있는 것을 알 수 있다. 


![](https://velog.velcdn.com/images/sharphand1/post/6cf2d58a-d530-41fd-a10d-19070cb0a4fc/image.png)

도대체 왜지???? 


```
const svg = d3.select("svg");
console.log('d3',d3)
console.log('svg',svg)
const width = Number(svg.attr("width"));
const height = Number(svg.attr("height"));
console.log(width,height)
```


D3.js(Data-Driven Documents) : 웹브라우저 상에서 동적이고 인터렉티브한 정보시각화를 구현하기 위한 자바스크립트 라이브러리.

여기서 svg가 검색창이 들어가면 달라진다!!??

잠만 svg의 nameSpace가 겹치는 것 같다.

namespaceURI: "http://www.w3.org/2000/svg"
뭔가 전역에서 겹치는 문제인가? 


svg의 원리를 모르겠다. 아니 왜 겹치는거야?? 그래서 안된다. 


script의 속성 

브라우저가 스크립트를 문서 분석 이후에, 그러나 DOMContentLoaded 발생 이전에 실행해야 함을 나타내는 불리언 속성입니다.
integrity
사용자 에이전트가 가져온 리소스에 예기치 못한 변형이 존재하는지 검사할 때 사용할 인라인 메타데이터입니

1/28


svg에 id를 추가해서 고유값을 줘보자 전역에서 겹치는 문제 해결하기 우해 element.setAttribute("id","graph");

const svg = d3.select("svg");
const svg = d3.select("#graph");로 변경


해결 -> 왜 겹치지. 현재 검색기능의 searchBox 내부에 버튼 태그 안에 svg가 들어가있는데 그래프의 d3.select("svg")가 검색기능 버튼안에있는 svg를 select하고 있어서 검색 기능을 넣으면 그래프가 보이지 않는 문제가 발생한 것이었다. 하... 둘이 nameSpace가 같아서 그런가? 이유를 찾아봐야겠다. 우선 문제는 해결! 

-> 우선 d3 window안에 저장됩니다.




문제 그래프랑 댓글이 늦게 뜨는 상황 
script를 비동기적으로 받아와서 뿌려주면 안되나? 




### 문제 : 검색창 / 입력 후,모든 값을 지워도 result가 사라지지 않습니다.

#### 원하는 상황 : 입력을 지웠을땐 결과가 없도록 하고 싶습니다.

**현재 상황** : 사용자가 "a"를 입력했다가 지운다면 당연히 a의 결과물이 보이지 않아야할 것 같습니다. 하지만 현재 저의 검색창은 한번 results가 보이면 사라지지 않는 문제가 발생했습니다. 

![](https://velog.velcdn.com/images/sharphand1/post/63b527da-fe77-4428-90f0-4cd0b9d23a1e/image.gif)

- 현재 코드
```js
const search = instantsearch({
	indexName: "digitalGarden",
		searchClient,
		searchFunction(helper) {
			if (helper.state.query) {
				helper.search();
			}
		},
	});
```

- 수정한 코드 
```js
	const search = instantsearch({
		indexName: "digitalGarden",
		searchClient,
		searchFunction(helper) {
			const container = document.querySelector("#hits");
			container.style.display = helper.state.query === "" ? "none" : "";
			helper.search();
		},
	});
```

#### 문제 해결 
id가 hits인 돔요소에 접근하고 helper.state.query가 비어있으면 display:none으로 되도록 만들고 아니면 helper.search()하도록 로직을 만드니 해결했습니다.


생각보다 어려워보이는 문제가 기본적인 지식으로 해결되는 것을 경험하고 있습니다. 참고로 console.log(helper)를 통해서 함수의 인자인 helper 객체 안에 어떤 key들이 있는지 확인하고 공식문서를 한시간 가량 찾다보니 해결할 수 있었습니다. 

**결과물 **
![](https://velog.velcdn.com/images/sharphand1/post/150a79c5-257a-4265-8047-6e01253213a5/image.gif)



### 문제 : 한번에 최대 20개의 결과가 나옵니다.

#### 원하는 상황 : 대략 5개 정도만 보여주고자 합니다. 

**현재상황**
![](https://velog.velcdn.com/images/sharphand1/post/ee26c572-2c4b-493a-8a64-0df9f1418f9e/image.png)

공식문서를 통해 transformItems 라는 함수가 있다는 것을 알게 됐습니다.UI에 그려지기 전에 hitted items를 받고 가공해서 새로운 배열로 리턴하는 역할을 한다고 합니다. 아이템들을 제거하고 변형하는데 유용하다고 합니다. 

![](https://velog.velcdn.com/images/sharphand1/post/09b99d1a-91a4-4419-b52a-6aeecbdf5bca/image.png)
출처: https://www.algolia.com/doc/api-reference/widgets/hits/js/


역시 베포 문제


![](https://velog.velcdn.com/images/sharphand1/post/5ab4abc8-f18c-412d-a2d2-3aabff52ecec/image.png)

백링크 관련 플러그인 삭제를 다해버려서 그런가? 

```
    File.write('_includes/notes_graph.json', JSON.dump({
      edges: graph_edges,
      nodes: graph_nodes,
    }))![업로드중..](blob:https://velog.io/23ab292d-a5da-481f-abe1-cf24e61d67d4)

```

해결 과정
백링크 중 file.write는 추가해서 알고리아 익덱스에 추가해보고 되면 베포해보는 바업ㅂ

#### 문제 해결 
생각처럼 동작하지 않았습니다. 우선 다른 문제부터 해결하기로 결정했습니다. 먼저 하단의 모든 페이지를 가리기에 해당 hits 영역에 height 고정값주고 overflow-y : scroll로 스크롤로 기능으로 대체하였습니다.



### how it works? 

1. parses generated HTML
2. split by paragraph
3. Pushes to Alogolia




[검색 기능 보러가기](https://juyoungdev.com/)


## 참고 자료


algolia API 모음집 : https://www.algolia.com/doc/api-reference/widgets/instantsearch/js/

50분 컨퍼런스 발표 영상 : https://www.youtube.com/watch?v=mnySRW94NL4
algolia github : https://github.com/algolia/jekyll-algolia

algolia community : https://discourse.algolia.com/


    