1. print() 의 두가지 옵션
	- sep= "" : 이 옵션을 이용하게 되면 print문의 출력문들 사이에 해당하는 내용을 넣을 수 있습니다. 기본 값으로는 공백이 들어가 있으며 이를 사용해 원하는 문자를 입력할 수 있습니다.
	- end= " " : 이 옵션의 경우 print 문을 이용해 출력을 완료한 뒤의 내용을 수정할 수 있습니다. 기본 값으로는 개행(\n)이 들어가 있으며 이를 사용해 개행을 없애거나 원하는 문자를 입력할 수 있습니다.
2. [for문] range() 함수는 숫자를 넣었을떄 리스트로 만들어주는 파이썬 내장 함수
3. [for문의 입력] input()대신 sys.stdin.readline()을 사용하는 이유
	- 한 두줄 입력받는 문제들과 다르게, 반복문으로 여러줄을 입력 받아야 할 때는 `input()`으로 입력은 에러
4. [for문] range함수의 세번째 인자에 -1을 넣으면 js에서 i--와 비슷하다.
5. [아스키코드] ord() 함수는 아스키코드로 chr()함수는 넘버로 
6. [ord] 대문자는 65 ~ 90 소문자는 97-122
7. [문자열 뒤집기] 문자열 그 자체를 뒤집는 것은 s[::-1]로 하면된다. 문자열[시작:끝:규칙]
8. [문자열 처리] 한글의 유니코드는 44032부터 시작. 
9. [유니코드 함수 암기] ord(문자) : 정수를 반환 chr(97) : a를 반환 
10. [spread 연산자와 비슷 ] ''[*quick_sort(lesser), pivot, *quick_sort(greater)]''
11. [print()] 파이썬에서는 print()는 자동적으로 줄바꿈을 해준다. 
12. [합계 점화식] :  1~ 10000까지의 숫자가 순서대로 있는데 이 땐 `n*(n+1) // 2`  해당 n과 다음 n을 곱하고 나누면 된다.
13. [표현식]
```python
    if n > m  : 
        if  n % m == 0 :
            print('multiple')  
        else :
            print('neither')
    else : 
        if  m % n == 0 :
            print('factor')
        else :
            print('neither')

print('factor' if b % a == 0 else 'multiple' if a % b == 0 else 'neither')
```
14. [음수를 양수로 나눈 후 나머지] % 연산자의 특징 
```python
-1 % 4 = 3
```
-1를 4로 나눈 나머지는 -1를 4로 나눈 나머지와 4가 같거나 작은 수 중에서 가장 큰 수를 4로 뺀 나머지와 같다 
나머지는 항상 양수여야한다는 특징 그래서 0이 아니라 3이 된다. 
-> 나머지 연산자의 결과값은 항상 양의 정수여야한다. a가 음수일 
```python
a % b == a - (a // b) * b
```
이 성립한다. 

15. [영어 소문자 문자열 비교] 
```python
# 내코드
t = int(input())

list = [0] * 26

for i in range(t) :
    name = input()
    last_name = name[0]
    list[ord(last_name)-97] += 1


if max(list) < 5 :
    print('PREDAJA')
else : 
    result = ''
    for i in range(len(list)) :
        if list[i] > 4 : 
            result += chr(i + 97)
    print(result)

# 다른 사람 코드 
arr = [input()[0] for _ in range(int(input()))]
f = 1
for i in range(97, 123):
    if arr.count(chr(i)) >= 5:
        f = 0
        print(chr(i), end='')

if f: print('PREDAJA')
```

16. [문자열 순서]string[::-1] 하면 된다.
-> [시작 : 끝 : 순서]
17. [입출력] map 
```python
A,B = map(list,sys.stdin.readline().split())
```
맵 안에 list를 넣으면 string이 split()돼서 나온다


18. [재귀 함수 리밋 설정] 파이썬의 기본 재귀 한도는 1000 그래서 1000을 넘길때는 모듈을 추가해준다. 
```python
import sys
sys.setrecursionlimit(10000)
```


19. [소수점 컨트롤]
```python
print(f'{more_aver_num / num * 100 :.3f}%')
```

20. [중복 순열]  itertools의 product 라이브러리

21. [Boolean] True로 연산도 가능하다 
```python
a = True + True + True
print(a) ## 3
```

22. [sort] word.find
```python
word = 'abdceaa'
print(sorted(word, key=word.find))
## a a a b d c e 
```

23. [boolean] :
```python
-   any() : 하나라도 True인게 있으면 True
-   all() : 모두 True여야 True 반환
```
