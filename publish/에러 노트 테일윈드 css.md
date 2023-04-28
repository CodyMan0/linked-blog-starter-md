1. [컴포넌트]path에 따라서 스타일을 다르게 줘야하는데 동적 할당을 해야한다. 
```ts
	let width: { [key: string]: string[] } = {
		'/sign-up/registration': ['mb-4 w-full lg:w-1/3'],
		'new-project': ['w-20', 'w-30', 'w-60']
	};
```

객체를 만들어주고 class에 직접 객체에 접근해서 가지고 오는 방식으로 해결 