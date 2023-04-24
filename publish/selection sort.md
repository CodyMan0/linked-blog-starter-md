순회하면서 최솟값을 가장 맨 앞에 두는 정렬 알고리즘 

성능 : O(n2)
- python
```python
array = [7,5,9,0,3,1,6,2,4,8]

for i in range(len(array)) :
	min_index = i
	for j in range(i+1, len(array)) :
		if array[min_index] > array[j] :
			min_index = j
	array[i] , array[min_index] = array[min_index] , array[i]

print(array)
```
- js
```js
function SelectionSort(arr) {
	for (let i = 0; i < arr.length - 1; i++) {
		let minValueIndex = i;
		for (let j = i + 1; j < arr.length; j++) {
			if (arr[j] < arr[minValueIndex]) {
				minValueIndex = j;
			}
		}

		let temp = arr[i];

		arr[i] = arr[minValueIndex];

		arr[minValueIndex] = temp;
	}
}

let arr = [4, 2, 1, 3];

SelectionSort(arr);

console.log(arr);

```

## 장단점
버블 정렬과 동일 


![[selectionSortDrawing.excalidraw.png]]

