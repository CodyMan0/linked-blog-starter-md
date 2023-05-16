---
sovledDay : 2023-05-09
time: 
review : 
reference : 
---

# DFS,BFS
## 2023-05-09 10:44 

```python
from collections import deque
# 1번 부터 N번 

# 입력 정점 개수 1부터 1000, 간선 개수 (1부터 1만 ), v (시작) 

n,m,start = map(int,input().split())
graph = [[False] * (n + 1) for _ in range(n+1)]

for _ in range(m) :
    a,b = map(int,input().split())
    graph[a][b] = True
    graph[b][a] = True

visited1 = [False] * (n+1)
visited2 = [False] * (n+1)

def dfs (v) :
    visited1[v] = True
    print(v, end=" ")
    for i in range(1,n+1) :
      if not visited1[i] and graph[v][i]:
        dfs(i)

    
def bfs (start) :
    queue = deque([start])
    visited2[start] = True
    while queue : 
        start = queue.popleft()
        print(start, end=" ")
        for i in range(1,n + 1) :
          if not visited2[i] and graph[start][i]:
            queue.append(i)
            visited2[i] = True
    


dfs(start)
print()
bfs(start)
```


## bfs 풀때 중요한 포인트
1. 탐색한 노드는 방문 처리 (불리언으로 해도 되고 0 , 1로 해도되는 듯)
2. 상하 좌우 방향에 대한 조건 처리 
3. bfs 함수를 만들고 적적하게 이중 리스트 포문 안에서 방문 처리가 되지 않은 애들에 한해 bfs 함수를 호출해야한다. 
4. 