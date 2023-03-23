[4,1,5,3,6,2]

정렬된 영역 : 4
비정력 : 1,5,3,6,2

삽입할 데이터: 1
정렬된 영역이 더 크니 , 정렬된 영역 인덱스에 붙혀넣고 4을 뒤로 복사 


핵심
정렬된 영역과 정렬되지 않은 영역 비교 
정렬되지 않은 영역 첫번째를 정렬된 영역 마지막 인덱스부터 차례대로 비교 후 정렬된 영역의 인덱스가 더 큰 숫자라면 덮어씌고 아니라면 해당 인덱스 뒤에 정렬되지 않은 영영의 인덱스를 삽입 

```js
function InsertionSort(arr) {
	for (let i = 1; i < arr.length; i++) {
		let insertingData = arr[i];
		let j;
		for (j = i - 1; j >= 0; j--) {
			if (arr[j] > insertingData) {
				arr[j + 1] = arr[j];
			} else {
				break;
			}
		}
		arr[j + 1] = insertingData;
	}
}
```