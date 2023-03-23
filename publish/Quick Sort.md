귀한 번 진행될 때마다 피벗이 정렬되고 정련된 배열을 좌우로 나눠서 같은 방식으로 재귀호출을 하여 모든 배열을 정렬시킨다. 

## 성능 
피벗 설정이 잘 돼있다면쎄베타(nlogn) 아니라면 O(n2)


## 구현
```js
function quickSort(arr, left, right) {
	if (left <= right) {
		let pivot = divide(arr, left, right);
		quickSort(arr, left, pivot - 1);
		quickSort(arr, pivot + 1, right);
	}
}

function divide(arr, left, right) {
	let pivot = arr[left];
	let leftStartIndex = left + 1;
	let rightStartIndex = right;
	while (leftStartIndex <= rightStartIndex) {
		while (leftStartIndex <= right && pivot >= arr[leftStartIndex]) {
			leftStartIndex++;
		}

		while (rightStartIndex >= left + 1 && pivot <= arr[rightStartIndex]) {
			rightStartIndex--;
		}

		if (leftStartIndex <= rightStartIndex) {
			swap(arr, leftStartIndex, rightStartIndex);
		}
	}

	swap(arr, left, rightStartIndex);
	return rightStartIndex;
}

function swap(arr, index1, index2) {
	let temp = arr[index1];
	arr[index1] = arr[index2];
	arr[index2] = temp;
}

let arr = [5, 3, 7, 2, 4, 1, 9, 0];

console.log("+======+");

console.log(arr);

quickSort(arr, 0, arr.length - 1);

console.log("정렬후");

console.log(arr);

```
