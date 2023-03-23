---
aliases: []
tags : 
---

출처 : 노마드 코더 
저자 :니코 
URL : 
인용 : 

왜 써야하나?
useForm을 사용하지 않으면 그 수 많은 인풋의 모든 스테이트를 관리해야한다. 그래서 무조건 써야한다. 그리고 Form validation이 필요해서

[useForm 도입 이유](https://tech.inflab.com/202207-rallit-form-refactoring/react-hook-form/)
# 1. useForm
 - ==register== : onChange의 역할을 해준다.  -> 그말은 인풋에 해당하는 state를 관리할 필요가 없다는 뜻  
-> 레지스터 만들면 input에 props를 안 넣어줘도 되고 자동으로 state를 관리해준다. 
 - ![[스크린샷 2022-09-29 오전 7.26.18.png]]
 - **watch** 함수를 통해서 onChange 되는 VALUE를 console.log()로 볼 수 있다.
 - **handleSubmit** 을 통해 validation을 검증할 수 있는 함수 
	- validation에 부합한 것은 handleSubmit()안에 있는 인자함수가 발동!
	- required를 왜 input의 property로 넣지 않고 register에 넣는지? 보안! 
	- Required의 조건이 맞지 않는 곳으로 바로 자동 focus가 간다.
- **formState** 을 통해 validation에 맞지 않아 생기는 에러들이 담긴다

## 1.1 useForm

`useForm` is custom hook for managing forms with ease. It takes **optional** arguments.

-   register
-   handleSubmit
-   watch
-   formState
-   getValues

```jsx
import React from "react";
import { useForm } from "react-hook-form";

export default function App() {
  const { register, handleSubmit, watch, formState: { errors } } = useForm();
  const onSubmit = data => console.log(data);

  console.log(watch("example")); // watch input value by passing the name of it

  return (
    /* "handleSubmit" will validate your inputs before invoking "onSubmit" */
    <form onSubmit={handleSubmit(onSubmit)}>
      {/* register your input into the hook by invoking the "register" function */}
      <input defaultValue="test" {...register("example")} />
      
      {/* include validation with required or other standard HTML validation rules */}
      <input {...register("email", { required: true, })} />
      {/* errors will return when field validation fails  */}
      {errors.exampleRequired && <span>This field is required</span>}
      
      <input type="submit" />
    </form>
  );
}
```


## register 사용법
![[스크린샷 2022-09-30 오후 4.02.24.png]]


### 생각의 연결고리
분야 :

키워드 :

관련있는 메모 : 