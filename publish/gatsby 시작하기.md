

### Install

-   gatsby-cli install

```
yarn global add gatsby-cli
```

-   프로젝트 생성

```
gatsby new [프로젝트 이름]
```

-   해당 프로젝트에서 typescript install

```
npm i -D typescript  
npm i gatsby-plugin-typescript
```


- gatsby-config plugin에 추가
```
* @type {import('gatsby').GatsbyConfig}

module.exports = {

plugins: [`gatsby-plugin-typescript`],

};
```


- tconfig.json 추가 
```
tsc --init
```

- tconfig.json 파일 수정 

gatsby의 버젼은 18버젼과 호환이 된다. 노드 버젼 업데이트 후 프로젝트 시작 

## 기초 공부 
**next.js v12와 비슷**
/project/**
![[스크린샷 2023-03-09 오전 10.00.04.png]]


- nav 바 
/src/components 에NavBar.js 컴포넌트를 만들고 필요한 페이지에 가져다가 쓰면 된다.


- layout component 

- static file 
#### 특징

##### 1
-> static 폴더에 들어간 파일은 public에 저장된다
-> static 폴더에 들어간 파일은 파일 경로로 찾아서 들어갈 수 있다.
-> 백앤드에서는 이렇게 하려면 static 뭐시기 코드 써야했는데 


##### 2. page에서 static에 접근하는 방법  


- graphQL and content mesh 
[[graphQL]]

-> graphQl API  
하는 법 
-> graphQl Query 
```ts

//gatsby.config.js
module.exports = {
	plugins: [`gatsby-plugin-typescript`],
	siteMetadata: {
		title: "codyMan",
		description: "web dev portfolio",
		},
	};

// pages/index.js
export const query = graphql`
	query SiteInfo {
		site {
			siteMetadata {
			title
			description
			}
		}
	}
`;
// page 컴포넌트 하단에 쿼리를 쿼리 스키마를 작성하면 해당 컴포넌트는 Prop로 data를 받게 된다 

  
const Home = ({ data }: Props) => {
	const { title, description } = data.site.siteMetadata;
	console.log(title); // codyMan
	
	return (
	<Layout>
	<div>Hello world!</div>
	</Layout>
	);
};

```
이런식으로 컴포넌트가 마운트되기전에 미리 static하게 데이터를 받을 수 있다는 것을 알게 됐다. 


##### 3. page가 아닌 디렉토리에서 데이터를 쿼리하는 법 
 useStaticQuery는 빌드 타임에 GraphQL 데이터를 사용할 수 있게 하는 리액트훅이다.

Error
 > The result of this StaticQuery could not be fetched.

-> 쿼리의 이름이 동일하면 안된다. 

4. 페이지 쿼리랑 static query랑 차이점
static query는 변수에 담길 수 없지만 어디서든 사용할 수 있고 페이지에서도 사용할 수 있다. 



##### 4. plugin 

1. gatsby-source-filesystem
2. gatsby-transformer-remark
3.  


4. gatsby-garden
-> 옵시디언 찾음!! 가자 !! 




##### 5. image 최적화 
1. gatsby-image
![[스크린샷 2023-03-18 오후 8.02.42.png]]
