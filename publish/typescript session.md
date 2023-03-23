# 왜 써야하나


### 1) 안전하니까


자바스크립트는 동적 타입 언어입니다. 런타임에 실제 코드의 값이 평가 될 시점에서야 이 변수에 들어올 값과 타입을 알 수 있다는 뜻입니다.

아래 코드에서 `num1`, `num2` 변수의 타입은 무엇일까요? 코드만으로는 런타임에 어떤 값이 들어올지 알 수 없으니 맞추는 건 애초에 불가능합니다. 변수의 이름만으로 추측해 볼 따름입니다.

```jsx
function multiply(num1, num2) {
  let result = num1 * num2;
  return result;
}
```

반면 정적 타입 언어들은 컴파일 타임에 변수의 타입을 결정합니다. 그러니 굳이 실제 코드를 실행해보지 않더라도 이 변수의 값이 무슨 타입인지 빌드 타임에 미리 알 수 있죠.

개발자가 이 변수의 타입이 무엇일지를 코드 레벨에서 결정하도록 강제합니다. Java와 같은 정적 타입 언어는 아래와 같이 `args` 라는 변수에 어떤 값이 들어올지를 알려줘야 합니다.

```java
public class Main {
  public static void main(String[] args) {
    System.out.println("Hello World");
  }
}
```



물론 어느 회사든 입사자에게 이런 일을 시키지는 않겠지만, “까봐야 아는” 코드를 배포하고 혹시 문제가 터지지는 않을까 뜬눈으로 밤을 지새는 일은 충분히 가능한 일입니다.

뭔가 잘못했다면 매도 먼저 맞는게 맞듯이, 최소한 타입을 잘못 넣어서 생길 수 있는 이유는 사용자가 아니라 개발자에게서 터지는 것이 바람직합니다.

### 2) 편리하니까

하지만 단순히 안전하다는 이유만으로 기술을 도입해야 할까요? 만약 정말 안전한 코드를 작성할 수는 있지만 기존 개발 속도보다 10분의 1 수준으로 느려진다면, 이 기술을 써야 할까요? 이 정도의 차이라면 다시 한번 생각해보는게 좋을 것 같네요.

하지만 장담할 수 있는 사실이 있다면, 타입스크립트는 일단 한번 익숙해지고 나면 자바스크립트를 사용할 때보다 여러분의 개발 속도는 현격하게 빨라질 겁니다.

타입스크립트를 사용할 때의 가장 큰 혜택 두 가지만 꼽자면 **1) 자동완성** 과 **2) 문서화 기능** 이라고 할 수 있겠습니다. 어찌 보면 같은 기능이라고도 볼 수 있겠지만 조금 맥락이 다르니 나누어 설명해보겠습니다.

:: **자동완성**

우리가 타입스크립트를 처음 접할 때 **“타입스크립트는 자바스크립트의 수퍼셋”** 같은 어쩌라는 건지 모를 알쏭달쏭한 설명을 가장 흔히 듣습니다. 사실, 개발을 하는 입장에서 느끼는 타입스크립트는 **IDE에 타입 힌트를 줄 수 있는 도구**에 더 가깝게 느껴집니다. 고마워, 타입민수야!

![https://joshua1988.github.io/ts/why-ts.html#왜-타입스크립트를-써야할까요](https://joshua1988.github.io/ts/images/math-js.gif)



배열 안에 들어 있는 값이 number 타입이므로 타입스크립트는 arr 변수를 number[]로 추론했다

![arr을 순회하는 map()의 첫 번째 인자로 들어올 수 있는 인자의 타입은 number이므로 number 타입이 사용할 수 있는 메서드가 추천된다](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/29622f57-3bb2-4b01-b562-415bbd7b690b/Untitled.png)

arr을 순회하는 map()의 첫 번째 인자로 들어올 수 있는 인자의 타입은 number이므로 number 타입이 사용할 수 있는 메서드가 추천된다

타입을 잘 사용하면 직접 모든 코드를 작성하지 않고, IDE가 추론해준 선택지들 사이에서 고르는 방식으로 개발해나갈 수 있습니다. 물론 힌트를 잘못 주면 오답이 나오겠죠. ==여기서 포인트는 ‘추론’과 ‘힌트’==입니다.

==IDE(Visual Studio Code) 뒷단==에서 돌고 있는 ==LSP(Language Server Protocol)===에 의해 개발자가 작성된 코드의 타입이 실시간으로 체크됩니다. 그래서 가끔 타입 추론이 제대로 되지 않을 때는 아래 스크린샷과 같이 TS Server를 재시작해주기도 합니다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/91f37c41-e1fa-4517-a3d5-ead7498c24be/Untitled.png)

언어 서버는 코드를 ==AST(Abstract Syntax Tree)== 형태로 만들고, 규칙에 따라 정적 분석(실제로 실행해보지 않고 분석하는 것) 합니다. IDE는 언어 서버로부터 분석 결과를 전달 받고, IDE는 다시 코드 각 부분에 대해 언어 서버로부터 응답 받은 타입을 사용자에게 표시하게 됩니다.

너무 설명이 딥한 것 같기는 하지만 정적 분석의 컨셉을 이해한다면 마법처럼 보이는 많은 것들을 이해할 수 있게 됩니다. 이미 우리가 잘 쓰고 있는 ESLint나 Prettier 같은 도구들도 이러한 정적 분석의 원리를 이용한 것입니다.


이제 우리가 할 일은 이런 명탐정 TS가 일을 잘 할 수 있도록(추론) 중간 중간 적절한 타입(힌트)를 주는 것뿐입니다. 종종 우리가 설명을 잘 못해주는 것 뿐이지, 생각보다 타입스크립트는 말귀를 잘 알아 듣습니다.

실제 예제 코드를 보겠습니다.

첫 번째 함수(`foo`)는 가능한 모든 부분에 타입을 부여했고, 두 번째 함수(`foo2`)는 함수 인자에만 타입을 부여했습니다. 우리는 `hiHello` 에 아무런 타입을 부여하지 않았지만 foo2는 재미있게도 자동으로 string 타입을 리턴하는 함수로 추론되었습니다. hi와 hello의 타입을 알 수 있으므로 당연한 귀결입니다.

하지만 중간에 any가 들어오거나 잘못된 타입 단언(개발자가 타입스크립트에게 자기가 맞다고 우기는 것 - `as` , `!` 등)을 잘못 사용하게 되면 타입 추론에 빈틈이 생기게 되고, 결국 실행될 때는 자바스크립트로 실행되므로 런타임 에러라는 파국을 맞이합니다.

이러면 타입스크립트를 쓰는 의미가 상당히 반감되겠지요. 그러므로 우리는 최대한 타입스크립트의 추론 시스템에 몸을 맡기고 자연스럽게 개발하는 습관을 들이는 것이 좋습니다.

개인적으로 기술 과제에 any나 불필요해 보이는 타입 단언이 들어 있는 코드를 보면 마음 속으로 상당히 감점을 주고 있습니다. 거의 대부분의 경우에 any는 불필요하며, 굉장히 제한적인 범위 안에서만 쓰는 것이 좋기 때문입니다.

[[5 세션 중간 중간 나오는 귀한 지식]]

![any를 부여하자마자 foo2 함수의 리턴 타입이 any로 바뀌고 말았다](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/47e675d9-2b95-4aa4-9cda-abb2c2347fb9/Untitled.png)

any를 부여하자마자 foo2 함수의 리턴 타입이 any로 바뀌고 말았다

![내 눈!](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0608c58c-0b8d-4801-acd2-09762a4ad44b/Untitled.png)

내 눈!

**:: 문서화**

타입스크립트로 라이브러리를 사용하다보면 `@types/`라는 이름이 붙은 패키지들을 많이 설치하게 됩니다. 이러한 라이브러리는 타입 정보만을 모아놓은 라이브러리들입니다. `Definitely Typed` 라는 이름의 프로젝트로 [링크](https://www.typescriptlang.org/dt/) 를 타고 들어가보시면 이 프로젝트의 공식 문서를 보실 수 있습니다.

아무튼 실제 열어보게 되면 다양한 타입들이 빼곡히 적혀있는 것을 확인해볼 수 있고, 주석 뿐만 아니라 이렇게 작성된 타입들의 의존 관계를 통해 이 코드가 대략 어떤 값들의 형태를 다루게 되는지 코드 작성자에게 물어보지 않고도 자연스레 알 수가 있게 됩니다.

```tsx
// allow undefined, but don't make it optional as that is very likely a mistake
function useMemo<T>(factory: () => T, deps: DependencyList | undefined): T
```

```tsx
// TODO (TypeScript 3.0): ReadonlyArray<unknown>
type DependencyList = ReadonlyArray<any>;
```

```tsx
/////////////////////////////
/// ECMAScript Array API (specially handled by compiler)
/////////////////////////////

interface ReadonlyArray<T> {
    /**
     * Gets the length of the array. This is a number one higher than the highest element defined in an array.
     */
    readonly length: number;
    /**
     * Returns a string representation of an array.
     */
    toString(): string;
```

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e0de0e4f-3409-4bc6-93d5-49fc17e9e27c/Untitled.png)

심심하니 React에서 사용하는 HTML 기본 태그의 타입은 어떤 식으로 매겨져 있는지 살펴볼까요?

```tsx
// /node_modules/@types/react/index.d.ts
interface IntrinsicElements {
	// HTML
	a: React.DetailedHTMLProps<React.AnchorHTMLAttributes<HTMLAnchorElement>, HTMLAnchorElement>;
	// ...
}

type DetailedHTMLProps<E extends HTMLAttributes<T>, T> = ClassAttributes<T> & E;

interface AnchorHTMLAttributes<T> extends HTMLAttributes<T> {
  download?: any;
  href?: string | undefined;
  hrefLang?: string | undefined;
  media?: string | undefined;
  ping?: string | undefined;
  rel?: string | undefined;
  target?: HTMLAttributeAnchorTarget | undefined;
  type?: string | undefined;
  referrerPolicy?: HTMLAttributeReferrerPolicy | undefined;
}

interface HTMLAttributes<T> extends AriaAttributes, DOMAttributes<T> {
  // React-specific Attributes
  defaultChecked?: boolean | undefined;
  defaultValue?: string | number | ReadonlyArray<string> | undefined;
  suppressContentEditableWarning?: boolean | undefined;
  suppressHydrationWarning?: boolean | undefined;

  // Standard HTML Attributes
  accessKey?: string | undefined;
  className?: string | undefined;
  // ...
}
```

```tsx
// /node_modules/@types/react/global.d.ts
interface HTMLAnchorElement extends HTMLElement { }

interface HTMLElement extends Element { }

interface Element { }
```

대략 어떤 느낌으로 추상화 되어 있는지 알아볼 수 있습니다. 이런 구조를 알아두면 함수의 인자로 이벤트 객체를 받을 때 올바른 타이핑을 할 수 있겠죠?

```tsx
import { HTMLAttributes } from "react";

export interface ButtonProps extends HTMLAttributes<HTMLButtonElement> {
  /* etc */
}

function App() {
  // Property 'type' does not exist on type 'IntrinsicAttributes & ButtonProps'
  return <Button type="submit"> text </Button>;
}
```

![“같은 이벤트가 이벤트가 아니에요” “그걸 어떻게 아셨나요?” “제가 눈으로 직접 봤거든요 ㅎ”](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/61de5309-e731-41c0-9a6e-512355b4477e/Untitled.png)

“같은 이벤트가 이벤트가 아니에요” “그걸 어떻게 아셨나요?” “제가 눈으로 직접 봤거든요 ㅎ”

```tsx
interface FormEvent<T = Element> extends SyntheticEvent<T> { }

/**
 * currentTarget - a reference to the element on which the event listener is registered.
 *
 * target - a reference to the element from which the event was originally dispatched.
 * This might be a child element to the element on which the event listener is registered.
 * If you thought this should be `EventTarget & T`, see <https://github.com/DefinitelyTyped/DefinitelyTyped/issues/11508#issuecomment-256045682>
 */
interface SyntheticEvent<T = Element, E = Event> extends BaseSyntheticEvent<E, EventTarget & T, EventTarget> { }

//
// Event System
// ----------------------------------------------------------------------
// TODO: change any to unknown when moving to TS v3
interface BaseSyntheticEvent<E = object, C = any, T = any> {
  nativeEvent: E;
  currentTarget: C;
  target: T;
  bubbles: boolean;
  cancelable: boolean;
  defaultPrevented: boolean;
  eventPhase: number;
  isTrusted: boolean;
  preventDefault(): void;
  isDefaultPrevented(): boolean;
  stopPropagation(): void;
  isPropagationStopped(): boolean;
  persist(): void;
  timeStamp: number;
  type: string;
}
```

이 외에도 tsc가 컴파일러라는 점 때문에 컴파일(트랜스파일링) 과정에서 해줄 수 있는 여러가지 기능들이나, 타입 기능이 강화되면서 조금 더 객체지향의 개념들을 사용할 수 있게 되는 등의 장점이 있으나 이 이상의 부분들은 각자 알아서 보충해봅시다 :)