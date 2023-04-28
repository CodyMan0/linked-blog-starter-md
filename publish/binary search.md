
Up : [[knowledge_MOCs]]


범위를 반으로 좁혀가며 탐색하는 것을 이진 탐색이라고 한다. 


## 장점 
성능이 O(logn)으로 좋다. 

-   이진 탐색(이분 탐색) 알고리즘은 **정렬되어 있는 리스트에서 탐색 범위를 절반씩 좁혀가며 데이터를 탐색하는 방법**이다.
-> 느낌: 가운데부터 주소록 찾기 게임 같은 느낌. 절반씩 나눠서 찾는게 이진 탐색이구나
-   변수 3개(`start, end, mid`)를 사용하여 탐색한다. **찾으려는 데이터와 중간점 위치에 있는 데이터를 반복적으로 비교해서 원하는 데이터를 찾는 것**이 `이진 탐색`의 과정이다.

## 단점 
-   `이진 탐색`은 **배열 내부의 데이터가 정렬되어 있어야만 사용할 수 있는** 알고리즘이다.



정렬 알고리즘 시간 복잡도 
![[스크린샷 2023-01-14 오전 11.56.42.png]]
오른쪽으로 갈수록 성능이 안좋다.




## 단점을 보완한 자료구조
이진 탐색 트리 자료구조는 이진 탐색 알고리즘의 장점만 취한 자료구조 


## 코드 암기하자 
- python 
```python
def binary_search(array,target,start,end ):
    if start > end :
        return None
    mid = (start + end) // 2
    if array[mid] == target:
        return mid
    elif array[mid] > target :
        return binary_search(array, target, start,mid -1)
    else :
        return binary_search(array,target,mid+ 1, end)

n , target = list(map(int, input().split()))
array = list(map(int,input().split()))

result = binary_search(array, target, 0 ,n-1)
if result == None :
    print("원소가 존재하지 않습니다.")
else :
    print(result + 1)
```

2. 반복문 사용 (top-down)
```python
def binary_search(array, target, start,end) :
    while start <= end :
        mid = (start + end ) // 2

        if array[mid] == target:
            return mid
        elif array[mid] > target :
            end = mid -1
        else : 
            start = mid + 1
    return None

n , target = list(map(int,input().split()))
array = list(map(int,input().split()))

result = binary_search(array, target, 0 , n - 1)

if result == None :
    print("원소가 존재하지 않습니다.")
else :
    print(result + 1)
```



## 파라메트릭 서치 
최적화 문제를 결정 문제로 바꾸어 해결하는 기법 [[P_NP]]

'원하는 조건을 만족하는 가장 알맞은 값을 찾는 문제'



### 생각의 연결고리
분야 :

키워드 :

관련있는 메모 : [[big O]]
