# 함수

동일한 코드를 반복적으로 사용하지 않기 위해 재사용하는 하나의 방식인 함수 
```python
def 함수명(매개변수):
	실행할 소스코드
	return 반환 값
```

- 파이썬에서는 함수를 호출하는 과정에서 인자를 파라미터의 변수에 직접 지정할 수 있다.
```python
def add(a,b):
    return a + b

add(b = 1, a = 4)

```

- 전역 변수에 대한 참조를 global이라는 키워드로 하는구나? 
(js는 scope chaning으로 자동적으로 상위 스코프를 검색하는데 파이썬은 다르구나? )
```python
a = 0 

def func():
    global a
    a += 1

for i in range(10):
    func()

print('global',a)
```

## 람다 표현식
함수를 간단하게 작성하는 일련의 방법