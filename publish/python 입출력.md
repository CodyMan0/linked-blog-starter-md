# 입력 
## 한 줄의 문자열을 입력 
input() 

## 여러 개의 데이터를 입력(공백으로 구분)
```python
list(map(int, input().split()))
```
여러개의 데이터를 공백으로 나눈 배열로 바꾼 뒤, map을 이용해서 해당 배열의 모든 원소에 int() 함수를 맵핑하는 것. 최종적으로 그 결과물을 list()로 감싸주어 입력받은 문자열을 띄어쓰리고 구분하여 각각 숫자 자료형으로 저장하게 되는 것. 

## 입력을 빠르게 받아야 할때 (정렬, 이진탐색, 최단 경로)
sys 라이브러리 사용
```python
import sys
sys.stdin.readline().rstrip()
```

### 한개의 정수 입력
```python
import sys
a = int(sys.stdin.readline().rstrip())
```
여기서 주의할 것은 개행문자까지 a변수에 초기화된다는 것. 그래서 rstrip()을 해줘야한다

### 정해진 갯수 정수를 한줄에 입력
```python
import sys
a,b,c = map(int, sys.stdin.readline().split())
```

### 임의의 개수의 정수를 한줄에 입력 받아 리스트 저장
```python
import sys
a,b,c = list(map(int, sys.stdin.readline().split()))

```
### 임의의 정수 n줄을 입력받아 2차원 리스트에 저장
```python
import sys
data = []
n = int(sys.stdin.readline())
for i in range(n):
	data.append(list(map(int,sys.stdin.readline().split())))
```
### 문자열 n줄을 입력받아 리스트에 저장
```python
import sys
n = int(sys.stdin.readlint())
data = [sys.stdin.readline().strip() for i in range(n)]
```

# 출력
자바스크립트 백틱과 같이 변수와 함께 사용하는 방법은 파이썬에서는 print(f{})이다.


# 핵심 라이브러리
1. **내장 함수**
	1. input() 
	2. print()
	3. min() :최솟값
	4. max( one , two or more)
	5. sorted() or sorted([1,2,3,] , reverse =True)
	6. 리스트와 같은 iterable 객체는 기본적으로 sort() 내장 매소드를 가지고 있다. 

2. **itertools** : 파이썬에서 반복되는 형태의 데이터를 처리하는 기능을 제공하는 라이브러리. 순열과 조합 라이브러리를 제공한다. 
	1. permutations : iterable 객체에서 r개의 데이터를 뽑아 일렬로 나열하는 모든 경우 (순열)을 계산
	2. combinations : 조합
	3. product : 모든 경우 순열 계산 원소를 중복하여 뽑는다.
3. **heapq** : 힙 기능을 제공하는 라이브러리. 우선순위 큐 기능을 구현하기 위해 사용된다.
	1. 원소 삽입 : heapq.heappush()
	2. 원소 제거 :  heapq.heappop()
		
	
4. **bisect** : 이진 탐색 기능을 제공하는 라이브러리
	1. bisect_left() (OlogN)
	2. bisect_right() (OlogN)
	```python
	from bisect import bisect_left, bisect_right

	a = [1,2,4,4,8]
	x = 2

	print(bisect_left(a,x)) 
	print(bisect_right(a,x))
	```

5. **collections** : 덱 , 카운터등의 유용한 자료구조를 포함하고 있는 라이브러리
	1. deque
		- 파이썬에서는 디큐를 활용해서 큐를 구현한다고 한다. js에서는 기본 내장 매소드인 pop(), push()를 활용해서 구현했었는데.
		- 파이썬에서 append와 pop 매소드는 리스트 가장 뒤에 있는 원소를 기준으로 추가하고 삭제한다. 그래서 가장 앞에 있는 원소를 처리할때 시간 복잡도는 O(n)이 소요한다.  그래서 deque 사용
		- deque 사용하면 인덱싱, 슬라이싱은 할수 없지만 데이터의 시작 혹은 끝에 데이터 삽입하는게 효과적이다. 
		1. popleft() : 첫 원소 제거 
		2. pop() : 마지막 원소 제거 
		3. appendleft(x) : 첫 원소 삽입
		4. append(x): 마지막 원소 삽입
		- 그래서 파이썬에서 deque로 큐 자료구조로 이용할땐 선입선출이 될 수 있도록 append() 를 사용하고 popleft()를 사용하여 먼저 들어온 요소가 먼저 나가도록 구현한다. 
	2. Counter
		- 와... 리스트와 같은 iterable 객체 내부 원소가 몇번 등장했는지 알려준다.
		- 와... js로 했을때 구현하기 어려웠던 건데 python은 바로 해주네
		```python
		from collections import Counter

		counter = Counter(['red', 'blue', 'red','green','blue'])

		print(counter['blue'])
		print(dict(counter)) 
		#{'red': 2, 'blue': 2, 'green': 1}
		```
6. math : 필수적인 수학적 기능을 제공하는 라이브러리. 팩토리얼 , 제곱근, 최대공약수, 삼각함수 관련 함수부터 파이와 같은 상수도 포함하고 있다
	1. factorial()
	2. math.sqrt()
	3. math.gcd() : 최대 공약수
