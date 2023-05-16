
Up : [[knowledge_MOCs]]

출처 :
저자 :
URL : 
인용 : 

# D3


## this를 공부하고 처음 this 관련 문제를 만나다
```ts

		const node = d3
			.select(graphRef.current)
			.append("g")
			.attr("class", styles.node)
			.selectAll("g")
			.data(nodes)
			.join("g")
			.on("mouseover", function () {
				d3.select(this).style("opacity", 0.5);
				console.log("this", this);
			})
			.on("mouseout", function () {
				d3.select(this).style("opacity", 1); // set opacity back to 100%
			})
			.call(
				d3
					.drag()
					.on("start", dragStarted)
					.on("drag", dragged)
					.on("end", dragEnded)
			);
```

D3안에서 mouseover 이벤트가 발생되면 d3의 this를 참조해서 styling을 해줘야하는데 화살표함수로 구현했을땐 this값이 undefined가 나왔다. 그래서  자체적인 this를 가지는 함수 선언문을 활용하여 구현하니 해당 노드의 this를 잘 가지고 왔다! 오호

### 생각의 연결고리
분야 :

키워드 : [[this]],  [[arrow function]], [[next.js를 사용하여 이력서님 개인 웹페이지 만들기]]

관련있는 메모 :
