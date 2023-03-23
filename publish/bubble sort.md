[4,2,3,1]

[2,3,1,4]
4는 정렬 완료

[2,1,3,4]
3 , 4,정렬 완료

[1,2,3,4]
1,2,3,4 정렬 완료 


시간 복잡도 : O(n2)

```js
function BubbleSort(arr) {
	for (let i = 0; i < arr.length - 1; i++) {
		for (let j = 0; j < arr.length - i - 1; j++) {
			if (arr[j] > arr[j + 1]) {
				let temp = arr[j];
				arr[j] = arr[j + 1];
				arr[j + 1] = temp;
			}
		}
	}
}
console.log(BubbleSort([1, 2, 3, 4]));

```

## 장점 
이해와 구현이 간단하다 

## 단점
성능이 좋지 않다. 