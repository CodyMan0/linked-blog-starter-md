# 못푼 문제 모음 Note 


## 1. 자리수의 합 (인프런 자바스크립트 강의 문제 1.19)
N개의 자연수가 입력되면 각 자연수의 자릿수의 합을 구하고, 그 합이 최대인 자연수를 출력 하는 프로그램을 작성하세요. 자릿수의 합이 같은 경우 원래 숫자가 큰 숫자를 답으로 합니다. 만약 235 와 1234가 동시에 답이 될 수 있다면 1234를 답으로 출력해야 합니다.


### 1차 
```js
function solution(n, arr) {

let answer = 0,

max = Number.MIN_SAFE_INTEGER;

  

arr.forEach((el, i, arr) => {

console.log(el.length);

for (let j = 0; j < el.length; i++) {

answer += el.toString()[i];

console.log(answer);

}

});

return answer;

}
```

역시 이중 포문 밖에 생각이 나지 않았다. 

### 정답
[[What i have learned]]

숫자형을 활용한 코드 
```js
function solution(n, arr) {

let answer = 0,

max = Number.MIN_SAFE_INTEGER;

  

for (let x of arr) {

let sum = 0,

tmp = x;

while (tmp) {

sum += tmp % 10;

tmp = Math.floor(tmp / 10);

}

if (sum > max) {

max = sum;

answer = x;

} else if (sum === max) {

if (x > answer) answer = x;

}

}

return answer;

}
```

내장함수로 
```js
  

function solution(n, arr) {

let answer = 0,

max = Number.MIN_SAFE_INTEGER;

  

for (let x of arr) {

let sum = x

.toString()

.split("")

.reduce((a, b) => a + Number(b), 0);

if (sum > max) {

max = sum;

answer = x;

} else if (sum === max) {

if (x > answer) answer = x;

}

}

return answer;

}
```
## 2. 등수 구하기 다시 풀기 
## 3.모의고사 (완전 탐색) 
24일 주말에 다시 풀기
