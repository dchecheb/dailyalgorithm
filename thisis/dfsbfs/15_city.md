
## My Answer
최대한 책에 나온 bfs 예시랑 비슷하게 풀어봤다.
시간 초과 났다.
```python
from collections import deque
n, m, k, x = map(int, input().split())
graph = list()
for _ in range(m):
    graph.append(list(map(int,input().split())))

def bfs(graph,start,visited):
    queue = deque([start])
    visited[start] = True
    cnt = 0 # 거리
    while queue:
        v = queue.popleft() # 현재 노드
        for i in graph:
            if i[0] == v: # 현재 노드와 인접한 노드
                if not visited[i[1]]:
                    visited[i[1]] = True
                    queue.append(i[1])
        if cnt == k:
            result = sorted(list(map(str, queue)))
            break
        cnt += 1
    return result

visited = [False]*(n+1) # visited[1]: 1번 노드
result = bfs(graph, x, visited)
print(" ".join(result))
```