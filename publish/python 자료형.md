# 정수형 실수형 복소수형

- 정수형 
```python
a = 1000
print(a)
```
- 실수형(소수점 아래의 데이터를 포함하는 수 자료형)
```python
a = 5.
print(a) // 5.0
```
-> 지수 표현 방식 (유효 숫자e 지수 = 유효숫자 *10 지수)
-> 지수 표현 방식은 실수로 처리된다. 

## 수자료형의 연산
1. 파이썬에서 나누기 연산자는 나눠진 결과를 실수형으로 반환한다.
2. 파이썬에서는 몫 연산자가 있다. (//)


- 복소수형




# 리스트
여러 개의 데이터를 연속적으로 담아 처리하기 위해 사용하는 자료형이다.
리스트가 굉장히 강력하다. 일반적인 배열에 이어 연결 리스트의 속성을 제공한다. 

## 리스트 초기화 
list() 혹은 []로 초기화해야한다. 
```python
a = [0] * n
[0,0,0,0,0 ...]
```
자바스크립트에선 Array.from({},) 이런식으로 했는데 


## 슬라이싱
슬라이싱을 제공한다. 연속적인 위치의 값 
자바스크립트에서 slice와 동일!!!
```python
a = [1,2,3,4]
print(a[1:4]) // 2,3,4
```

## 리스트 컴프리헨션
내부적으로 반복문과 조건문을 포함할 수 있다. 
```python
a = [i for i in range(20) if i % 2 == 1]

print(a)

a = [i * i for i in range(1,10)]

print(a)
```

리스트 컴프리헨션은 2차원 리스트를 초기화할때 효과적으로 사용될 수 있다. 
특히 N*M 크기의 2차원 리스트를 한번에 초기화 해야할때  유용하다 


### 언더바 사용 이유
반복을 수행하되 반복을 위한 변수의 값을 무시하고자 할때 언더바를 사용한다

```python
for _ in range(5):
  print("Hello world")
```
![[스크린샷 2023-04-09 오후 8.54.29.png|500]]
append() : 가장 뒤에 요소 하나를 추가할때 사용한다. O(1)
sort() :  O(nlogn)
reverse() : O(n)
insert() : O(n)
count() : 특정 값을 가지는 데이터의 수를 셀때 매소드 O(n)
remove() : 특정 값을 제거하는데 사용된다. 만약 여러개가 있다면 한개만 제거하는 특징이 있다. O(n)

# 문자열 튜플
- 문자열
"", ' '은 js랑 동일하다 
js에서 변수를 넣을 수 있게 하는 기호는 파이썬에서는 뺵슬래쉬 같다

### 문자열 연산
- 덧셈
-> 문자열끼리 더하면 문자열이 더해진다
- 곱셈
-> 양의 정수와 곱하면 정수만큼 문자열이 길어진다. 


### 문자열 포매팅
```js
const number = 21
const test = `my age is ${number}`
```

```python
# 문자 포맷팅
## 숫자 바로 대입
print("I eat %d apples" % 3)

## 문자열 바로 대입
print("I eat %s apples" %"five")

## 2개 이상 대입
number =10
day = "three"
print ("I ate %d apples. so i was sick for %s days" %(number , day))


## format 함수로 포매팅
print("I eat {0} apples".format("three"))
print("I eat {0} apples during {1}days".format("three", 3))


## 공백 채우기
print("{0:=^10}".format("hi"))
```

이런식으로 문자열안에 변수를 삽입했는데 파이썬에서는 약간 다른 것 같다. 어제는 print(f)이 동일한 개념이겠거니 했으나 다르다는 것을 오늘 알게 됐다.


### 문자열 내장 함수
1. count : 특정 문자열과 동일한 문자열의 갯수 반환
2. find : 특정 문자열의 첫 인덱스 반환 없으면 -1
3. index : find와 동일하지만 반환이 없으면 에러 발생시킴
4. join : 문자열 삽입
5. upper() : 대문자로
6. lower(): 소문자로
7. lstrip() : 왼쪽 공백 없애기 
8. rstrip() : 오른쪽 공백 없애기 
9. replace() : 문자열 바꾸기
10. split() : 문자열 나누기

# 튜플
리스트와 유사하지만 한번 선언된 값을 변경할 수 없다는 특징이 있다.  (문자열과 동일한 원리 )
리스트는 대괄호 튜플은 소괄호를 이용한다 
튜플은 리스트보다 기능이 제한적이어서 공간이 효율적이다. 

### 사용처
1. 서로 다른 성질의 데이터를 묶어 사용할떄 (최단경로에서 비용을 실수 , 노드번호는 정수형으로 )
2. 데이터의 나열을 해싱의 키 값으로 사용해야 할때 
3. 튜플은 변경이 불가해서 리스트와 다르게 키 값으로 사용될 수 있다.



# 사전 자료형
==js의 map()과 동일==
key와 value로 이루어진 쌍 (순서가 정해지지 않는다.)
파이썬은 사전 자료형 자체가 hash Table로 이루어져있어 데이터 조회, 수정에서 O(1)의 성능을 보인다.

```python
data = dict()

data['사과'] = 'Apple'

print(data)

if '사과' in data:
  print('사과를 키로 가지고 있어요')
```

- 키와 value를 각각 뽑아내기 위해 매소드를 지원한다
키는 keys() 값 데이터는 values()

# 집합 자료형
==js의 set()과 동일==
중복을 허용하지 않는다. 
순서가 없다.
```python
data = set([1,1,1,1,2,3,4,4])

print(data)

data = {1,1,1,1,1,1,2}

print(data)
```


## 연산 제공
합집합 : |
교집합 : & 
차집합 : -

## 추가, 삭제 메소드
add 
update() : 여러개 추가
remove()

### 튜플과 리스트와의 사전, 집합 자료형의 차이
순서가 없기에 인덱싱으로 접근이 불가하고 key 값으로 접근할 수 있다는 것.
입력은 input()으로 
출력은 print()
print(f)는 js의 백스트링과 같다.