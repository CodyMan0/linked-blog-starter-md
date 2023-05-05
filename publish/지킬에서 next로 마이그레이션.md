# idea
1. 노드 무한 이벤트 트리거 : stopPropagation()


# animation
- [x] 페이지 전환 에니메이션 
- [x] 로딩 기능 넣어서 UI/UX 기능 구현 
- [ ] 포인터 UI 그리고 애니메이션 주자 

# layout
- [x] 반응형 기본 footer, sidebar
 - [ ] 전역 공통 컴포넌트 project's detail layout
![[스크린샷 2023-04-10 오후 7.26.35.png|500]]


![[스크린샷 2023-04-10 오후 7.26.45.png|500]]
예배 아이디어
1. 나의 진로 설계도 맵을 구현해보자
2. 스크롤 이벤트로 목표를 위해 달려가는 이밎 표현


## 디자인
- [ ] 스펙을 첫 페이지에서 보여주면 좋을 것 같다.

## 상태관리 
/projects 라우트에서보이는 스텍은 현재 constant.ts라는 파일에서 데이터를 수정하면 반영이 되는데 여기 보여지는 데이터를 /projects/[...slug.tsx] 에 각각 데이터가 보여지게 하려면 어떻게 해야할까? 

![[스크린샷 2023-04-07 오후 7.33.26.png]]


-> 상태관리? 
-> 보이려고 하는 페이지에
```Js
import { PROJECT_LIST } from "../../lib/constants";
```

project_list 상수 객체를 불러와서 해당 key 값만 변형하여 쓸수 있으면 되지 않을까? 


d3 -> https://github.com/wchorski/nextjs-obsidian-publish



# CSS
- [ ] 글자가 짤리는데 css로 해결해보자! 
- [ ] 다크모드 색 전환  -> https://www.youtube.com/watch?v=YPkUczwF3mM

# SEO
- [ ] 페이지 마다 카카오톡 오픈 그래프로 이미지 설정하기 

# error
1. taillwind css의 동적 클래스 부여시 에러 in next.js 

개발 환경 
- next.js : "latest"
- "typescript": "^4.7.4"
- "tailwindcss": "^3.2.4"

하려고 하는 것 
![[스크린샷 2023-03-28 오전 9.33.47.png]]

오른쪽 특정 영역과 특정 영역 위에 이동시킬 카테고리가 보이는 재사용이 가능한 컴포넌트를 만들려고 합니다 

```js
//index.tsx
	{BLOCK_LIST.map((block) => {
				return (
					<BlockTemplate
						key={block.id}
						width={block.width}
						color={block.color}
						label={block.label}
					/>
				);
			})}

```

BLOCK_LIST라는 데이터 갯수 만큼 BlockTemplate 컴포넌트가 마운트됩니다.

```ts
//BLOCK_LIST 상수 
export const CMS_NAME = "Markdown";
export const HOME_OG_IMAGE_URL =
	"https://og-image.vercel.app/Next.js%20Blog%20Starter%20Example.png?theme=light&md=1&fontSize=100px&images=https%3A%2F%2Fassets.vercel.com%2Fimage%2Fupload%2Ffront%2Fassets%2Fdesign%2Fnextjs-black-logo.svg";

export const BLOCK_LIST = [
	{
		id: 1,
		width: "min-w-[40%]",
		color: "bg-slate-600",
		label: "ProjectName",
	},
	{
		id: 2,
		width: "min-w-[60%]",
		color: "bg-red-300",
		label: "About Me",
	},
	{
		id: 3,
		width: "min-w-[33.3%]",
		color: "bg-sky-500",
		label: "ProjectName",
	},
	{
		id: 4,
		width: "min-w-[33.3%]",
		color: "bg-violet-900",
		label: "ProjectName",
	},
	{
		id: 5,
		width: "min-w-[33.3%]",
		color: "bg-slate-200",
		label: "ProjectName",
	},
];
```
해당 데이터로부터 컴포넌트가 그려지도록 하였습니다.


```tsx
//BlockTemplate.tsx (자식 컴포넌트)

type Props = {
	label?: string;
	width: number;
	color: string;
	image?: string;
};

const BlockTemplate = ({ width, color, image, label }: Props) => {
	console.log(`위드 ${width} 컬러${color}`);


	return (
		<div
			className={`${width} ${color} h-64 relative`}
		>
			{image && "이미지"}
			<button className="bg-white z-10 absolute top-3.5 right-3.5 p-3 text-2xl font-bold border-2 border-black rounded-sm drop-shadow-lg">
				{label}
			</button>
		</div>
	);
};

export default BlockTemplate;

```


> 여기서 테일윈드가 적용이 되지 않는 에러가 발생하였습니다. 


수정한 부분 
1. 상수 객체 데이터 수정 (BLOCK_LIST)
```ts
export const BLOCK_LIST = [
	{
		id: 1,
		width: 40,
		color: "blue",
		label: "ProjectName",
	},
	{
		id: 2,
		width: 60,
		color: "red",
		label: "About Me",
	},
	{
		id: 3,
		width: 33.3,
		color: "yellow",
		label: "ProjectName",
	},
	{
		id: 4,
		width: 33.3,
		color: "pink",
		label: "ProjectName",
	},
	{
		id: 5,
		width: 33.3,
		color: "purple",
		label: "ProjectName",
	},
];

```

2. BlockTemplate 컴포넌트 수정 
```tsx
//BlockTemplate.tsx (자식 컴포넌트)

type Props = {
	label?: string;
	width: number;
	color: string;
	image?: string;
};

const BlockTemplate = ({ width, color, image, label }: Props) => {

	const widthVariants = {
		40: "min-w-[40%]",
		60: "min-w-[60%]",
		33.3: "min-w-[33.3%]",
	};
	const colorVariants = {
		blue: "bg-blue-600 hover:bg-blue-500",
		red: "bg-red-500 hover:bg-red-400",
		yellow: "bg-yellow-300 hover:bg-yellow-400 ",
		pink: "bg-yellow-300 hover:bg-yellow-400 ",
		purple: "bg-yellow-300 hover:bg-yellow-400 ",
	};


	return (
		<div
			className={`${widthVariants[width]} ${colorVariants[color]} h-64 relative`}
		>
			{image && "이미지"}
			<button className="bg-white z-10 absolute top-3.5 right-3.5 p-3 text-2xl font-bold border-2 border-black rounded-sm drop-shadow-lg">
				{label}
			</button>
		</div>
	);
};

export default BlockTemplate;

```

핵심적으로 보면 

```ts
className={`${width} ${color} h-64 relative`}
//width는 min-w-[33.3%] 하나의 속성을 전체로 넣어주었습니다. 
-> 
className={`${widthVariants[width]} ${colorVariants[color]} h-64 relative`}
//BlockTemplate 내부에 선언된 객체 widthVariants의 키값을 props로 받아 해당 컴포넌트에서 그려줍니다. 
```

이렇게 바꾸니 해결이 됐다. 왤까? 


3. 

https://fe-developers.kakaoent.com/2022/220303-tailwind-tips/


공부 과정 


