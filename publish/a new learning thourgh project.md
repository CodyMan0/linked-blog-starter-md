1. next/Link는 좀 다르다.
```ts
<Link href={{pathname: `/members/${id}`,
	query: {userInfo: JSON.stringify(member)}
	}}
	as={`/members/${id}`}
>
```

