1. [90도 회전 코드] 자물쇠와 열쇠
```python
def rotate_a_matrix_by_90_degree(a) :
    n = len(a)
    m = len(a[0])
    result = [[0] * n for _ in range(m)]
    for i in range(n): 
        for j in range(m) :
            result[j][n -i -1] = a[i][j]
    return result

```

2. [배열안에서 가장 많은 요소 선택 ] 
```python

def find_majority_element(lst):
    m = -1
    i = 0
    for j in range(len(lst)):
        if i == 0:
            m = lst[j]
            i = 1
        elif m == lst[j]:
            i += 1
        else:
            i -= 1
    return m
```