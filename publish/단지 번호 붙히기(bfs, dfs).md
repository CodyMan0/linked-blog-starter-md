---
sovledDay : 2023-05-12
time: 
review : 
reference : 
---

# 단지 번호 붙히기(bfs, dfs)
## 2023-05-12 13:09 


1. bfs
```python

import sys
from collections import deque

dx = [0,0,1,-1]
dy = [1,-1,0,0]

def bfs(graph, x, y) :
    n = len(graph)
    q = deque()
    q.append((x,y))
    graph[x][y] = 0
    cnt = 1
    while q : 
        xx , yy = q.popleft()
        for i in range(4) :
            nx = xx + dx[i]
            ny = yy + dy[i]
            if 0 <= nx < n and 0 <= ny < n :
                if graph[nx][ny] == 1 :
                    graph[nx][ny] = 0 
                    q.append((nx,ny))
                    cnt += 1
    return cnt 
                

n = int(input())
graph = []
for i in range(n) : 
    graph.append(list(map(int,input())))

count = []
for i in range(n):
    for j in range(n):
        if graph[i][j] == 1:
            count.append(bfs(graph,i,j))

count.sort()

print(len(count))
for i in range(len(count)):
    print(count[i])

```

1. 핵심 방문한 인덱스를 0으로 바꿔줘 중복되게 방문하는 것을 방지 
2. count 배열을 전역에 선언하고 graph가 1일때 graph와 i,j를 가진 bfs 함수가 실행되도록 한다.
3. bfs 내부에 count가 있고 큐가 참일 동안 네 방향을 순회하며 확인한다. 여기서 상하좌우 인덱스의 값이 1일때 방문하고 0으로 초기화하고 그 값을 큐에 넣어 반복해주고 마지막으로 1을 카운트해주면끝


2. dfs
```python
n = int(input())
graph = []
num = []

for i in range(n):
    graph.append(list(map(int,input())))

dx = [0,0,1,-1]
dy = [1,-1,0,0]

def dfs(x,y) :
    if x < 0 or x >= n or y < 0 or y >= n:
        return False
    if graph[x][y] == 1 :
        global count
        count += 1
        graph[x][y] = 0
        for i in range(4) :
            nx = x + dx[i]
            ny = y + dy[i]
            dfs(nx,ny)
        return True
    return False

count = 0
result = 0

for i in range(n):
    for j in range(n):
        if dfs(i,j) == True :
            num.append(count)
            result += 1
            count = 0

num.sort()
print(result)
for i in range(len(num)):
    print(num[i])
```