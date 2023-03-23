
## 직사각형 지갑 (프로그래머스 1.17)
[[new learning_algorithm]]
### 유형 공부 전 나의 풀이 
```js
function solution(sizes) {
    const copy = [...sizes];
    const sortedCopy = copy.map((el)=>{
        return sort = el.sort((a,b) => (a-b)) 
    })
    const pickOneFromBig = sortedCopy.map((el) => {
        return el[0]
    })

     const pickOneFromSmall = sortedCopy.map((el) => {
        return el[1]
    })

     return Math.max(...pickOneFromBig) * Math.max(...pickOneFromSmall)
}
```

### 유형 공부 후 나의 풀이 

## 자리수의 합 (인프런 자바스크립트 강의 문제 1.19)
N개의 자연수가 입력되면 각 자연수의 자릿수의 합을 구하고, 그 합이 최대인 자연수를 출력 하는 프로그램을 작성하세요. 자릿수의 합이 같은 경우 원래 숫자가 큰 숫자를 답으로 합니다. 만약 235 와 1234가 동시에 답이 될 수 있다면 1234를 답으로 출력해야 합니다.

## 뒤집은 소수
[[숫자 뒤집기.excalidraw]]

### 숫자 그자체로 바꾸는것
```js
const isPrime = (num) => {

if (num === 1) return false;

for (let i = 2; i < parseInt(Math.sqrt(num)); i++) {

if (num % i === 0) return false;

}

return true;

};

  

function solution(arr) {

let answer = [];

for (let x of arr) {

let result = 0;

while (x) {

let t = x % 10;

result = result * 10 + t;

x = parseInt(x / 10);

}

if (isPrime(result)) answer.push(result);

}

  

return answer;

} 


```

### 문자열로 변환
```js

function solution(arr) {

let answer = [];

for (let x of arr) {

let result = Number(x.toString().split('').reverse().join(''));
 
if (isPrime(result)) answer.push(result);

}

  

return answer;

}
```

 