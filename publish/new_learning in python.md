1. print() 의 두가지 옵션
	- sep= "" : 이 옵션을 이용하게 되면 print문의 출력문들 사이에 해당하는 내용을 넣을 수 있습니다. 기본 값으로는 공백이 들어가 있으며 이를 사용해 원하는 문자를 입력할 수 있습니다.
	- end= " " : 이 옵션의 경우 print 문을 이용해 출력을 완료한 뒤의 내용을 수정할 수 있습니다. 기본 값으로는 개행(\n)이 들어가 있으며 이를 사용해 개행을 없애거나 원하는 문자를 입력할 수 있습니다.
2. [for문] range() 함수는 숫자를 넣었을떄 리스트로 만들어주는 파이썬 내장 함수
3. [for문의 입력] input()대신 sys.stdin.readline()을 사용하는 이유
	- 한 두줄 입력받는 문제들과 다르게, 반복문으로 여러줄을 입력 받아야 할 때는 `input()`으로 입력은 에러
4. [for문] range함수의 세번째 인자에 -1을 넣으면 js에서 i--와 비슷하다.
5. [아스키코드] ord() 함수는 아스키코드로 chr()함수는 넘버로 
6. [문자열 뒤집기] 문자열 그 자체를 뒤집는 것은 s[::-1]로 하면된다. 문자열[시작:끝:규칙]
7. [문자열 처리] 한글의 유니코드는 44032부터 시작. 
8. [유니코드 함수 암기] ord(문자) : 정수를 반환 chr(97) : a를 반환 
9. [spread 연산자와 비슷 ] ''[*quick_sort(lesser), pivot, *quick_sort(greater)]''
10. [print()] 파이썬에서는 print()는 자동적으로 줄바꿈을 해준다. 
11. [합계 점화식] :  1~ 10000까지의 숫자가 순서대로 있는데 이 땐 `n*(n+1) // 2`  해당 n과 다음 n을 곱하고 나누면 된다.
12. [표현식]
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