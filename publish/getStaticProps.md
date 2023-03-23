1. SSG의 기능을 해주는 것

getStaticProps 매소드는 "빌드 타임"에 맨먼저 실행된다.



## 13버전에서는 /app에서 사용하지 못함

12버전

``` tsx
export async function getStaticProps() {

const delayInSeconds = 2;

const data = await new Promise(resolve =>

setTimeout(() => resolve(Math.random()), delayInSeconds * 1000)

);

return {

props: { data },

};

}
```

13버전
```ts
import React, { use } from 'react';

  

interface Props {

data: number;

}

  

const Page = () => {

const test = use(getData());

console.log(test);

return (

<main>

<h1>getStaticProps</h1>

<p>값 :{test}</p>

</main>

);

};

  

export default Page;

  

export async function getData() {

const delayInSeconds = 2;

const data = await new Promise(resolve =>

setTimeout(() => resolve(Math.random()), delayInSeconds * 1000)

);

console.log(data);

return data;

}
```
