# 반복문
특정한 소스코드를 반복적으로 실행하고자 할때 사용할 수 있다.
- for 문 (상대적으로 소스코드가 짧게 나온다.)
- while 문

## while 문
조건문이 참일 때에 한해서 반복적으로 코드가 수행되는 문

```python
i = 1
result = 0

while i <= 9:
  if i % 2 == 1:
    result += i
  i += 1

print(result)

```

## for 문
리스트를 사용하는 대표적인 구조 
```python
for variable in list :
	source code

result = 0

for i in range(1, 10):
	result += i
print(result)

# js에서는

for( let i = 0; i < list.length; i ++ ){
	sourceCode()
}

```
확실히 Js보다 더 간단한 것 같다. 

### 특징
1. range()의 값으로 하나의 값만 넣으면 시작 index는 자동으로 0. 
2. range(start, end) 두개의 값을 넣으면 start index 부터 end -1 Index까지 반복된다.