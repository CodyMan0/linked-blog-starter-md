💡정의 : 함수에 파라미터로 들어가는 함수
용도 : 순차적으로 실행하고 싶을때 씀

# callback은 비동기로만 사용되나?
아니다 synchronous ,asynchronous에 다 쓰인다. 


```js
/* callback */

function add10(a, callback){

setTimeout(() => callback(a + 10), 100);

}

​

add10(5, res => {

console.log(res); // 15

});
```

- promise 

```js
function add20(a){

return new Promise(resolve => setTimeout(() => resolve(a + 20), 100));

}


add20(5).then(console.log); // 25
```

## 문제
1. 가독성이 낮다.


### 관련 있는 메모
가독성의 문제를 해결한 [[Promise (js)]]
