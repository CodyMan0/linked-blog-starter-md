너비 우선 탐색이란 그래프 자료구조의 데이터를 탐색하는 방법 두가지중 첫번째! 

# BFS란 

## 개념 
1. 큐에 방문한 정점 기록 
2. 큐에서 디큐 
3. 디큐한 정점의 인접 정접을 순회한다. 
4. 


## 특징 
1. 방문한 기록은 해시테이블에 저장 그리고 BFS에서는 큐에도 저장 


## 성능 
O(V+E)

### python BFS
자료구조 큐를 활용하여 가까운 노드부터 탐색하는 알고리즘으로써 DFS와 반대의 알고리즘.  또한 탐색하는데 O(N)이 소요되고 일반적으로 DFS보다 약간 성능이 좋다는 점이 있다. 

1.  탐색 시작 노드를 큐에 삽입하고 방문처리를 한다.
2.  큐에서 노드를 꺼내 해당 노드의 인접 노드 중에서 방문하지 않은 노드를 모두 큐에 삽입하고 방문처리를 한다.
3.  2번을 더이상 수행할 수 없을 때까지 반복한다.

위의 로직을 아래와 같이 구현할 수 있다.
```python
from collections import deque

def bfs(graph,start,visited):
    queue = deque([start])
    visited[start] = True
    while queue:
        v = queue.popleft()
        print(v, end =' ')
        for i in graph[v] :
            if not visited[i] :
                queue.append(i)
                visited[i] = True


graph = [
    [],
    [2,3,8],
    [1,7],
    [1,4,5],
    [3,5],
    [3,4],
    [7],
    [2,6,8],
    [1,7]
]

visited = [False] * 9

bfs(graph , 1 , visited)
```








