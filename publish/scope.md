# 스코프란

스코프는 식별자 (변수, 함수, 클래스)가 참조될 수 있는 범위, 식별자를 검색하는 규칙을 의미한다.

## 함수레벨 
var 키워드로 선언된 변수나 함수 선언문으로 만들어진 함수는 함수레벨 스코프를 갖는다.

## 블록 레벨 스코프 
const, let 

## 렉시컬 스코프 
함수가 실행될 때 스코프를 어떻게 정의하는지에 따라 함수의 결과가 달라질 수 있다. 


###  2가지 방법인  렉시컬 vs 동적 스코프

1. **동적 스코프**는 프로그램의 런타임 도중의 실행 컨텍스트나 호출 컨텍스트에 의해 결정되고, 렉시컬 스코프에서는 소스코드가 작성된 그 문맥에서 결정된다. 현대 프로그래밍에서 대부분의 언어들은 렉시컬 스코프 규칙을 따르고 있다.

2. ==렉시컬 스코프 규칙을 따르는 자바스크립트의 함수==는 **호출 스택과 관계없이 각각의 (`this`를 제외한)대응표를 소스코드 기준으로 정의하고, 런타임에 그 대응표를 변경시키지 않는다.** (사실 런타임에 렉시컬 스코프를 수정할 수 있는 방법들(`eval`, `with`)이 있지만, 권장하지 않는다.)

## 그럼 어떻게 javascript는 scope들의 관계를 알 수 있을까?
[[scope chain]]


## 이러한 지식을 기반으로 실행 컨텍스트 이해하기
[[Execution Context]]



### 관련있는 메모 
[[closure (11.22)]]
[[Execution Context]]






