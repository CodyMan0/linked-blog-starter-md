> divide and conquer 

분할 정복을 통해 어려운 문제를 쪼갠 다음 해결하는 습관을 가지자

![[스크린샷 2023-03-20 오전 11.11.26.png]]





```js
function MergeSort(arr, leftIndex, rightIndex) {
	if (leftIndex < rightIndex) {
		let midIndex = parseInt(leftIndex + rightIndex / 2);
		MergeSort(arr, leftIndex, midIndex);
		MergeSort(arr, midIndex + 1, rightIndex);
		Merge(arr, leftIndex, rightIndex);
	}
}



function Merge(arr, leftIndex, midIndex, rightIndex) {
	let leftAreaIndex = leftIndex;
	let rightAreaIndex = midIndex + 1;

	let tempArr = [];
	tempArr.length = rightIndex + 1;
	tempArr.fill(0, 0, rightIndex + 1);

	let tempArrIndex = leftIndex;
	while (leftAreaIndex <= midIndex && rightAreaIndex <= rightIndex) {
		if (arr[leftAreaIndex] <= arr[rightAreaIndex]) {
			tempArr[tempArrIndex] = arr[leftAreaIndex++];
		} else {
			tempArr[tempArrIndex] = arr[rightAreaIndex++];
		}
		tempArrIndex++;
	}

	if (leftAreaIndex > midIndex) {
		for (let i = rightAreaIndex; i <= rightIndex; i++) {
			tempArr[tempArrIndex++] = arr[i];
		}
	} else {
		for (let i = leftAreaIndex; i <= midIndex; i++) {
			tempArr[tempArrIndex++] = arr[i];
		}
	}

	for (let i = leftIndex; i <= rightIndex; i++) {
		arr[i] = tempArr[i];
	}
}

```

가운데 기준으로 왼쪽과 오른쪽을 정렬한다. 







## 성능 
O(nlogn)



## 장단점
장점 : 성능이 좋다
단점 : 이해와 구현이 어렵다. 



### 관련있는 메모 
1. [[recursive function]]