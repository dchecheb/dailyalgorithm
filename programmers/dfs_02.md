# [네트워크](https://programmers.co.kr/learn/courses/30/lessons/43162)
dfs/bfs 문제.
네트워크 개수 세는 방식을 잘못읽어서 한참 돌아 풀었다.

## My Answer
깊이우선탐색 방식이다. 네트워크 연결된 컴퓨터를 깊이우선으로 모두 탐색한다. 그리고 연결을 확인한 네트워크는 0으로 초기화해주어, 다시 개수를 세지 않게 하였다. networks 리스트는 현재 탐색 중인 노드와 같은 망에 있는 노드들을 저장해두는 리스트다. 인트라넷이 아니라면 network를 -1 해주고 networks에 append한다.<br>

변수
```python
def solution(n, computers):
    global network
    network = n
    for i in range(len(computers)):
        for j in range(len(computers)):
            if i != j and computers[i][j]:
                networks = [i]
                computers = dfs(i, j, networks, computers)
    return network

def dfs(i, j, networks, computers):
    global network

    if j not in networks:
        network -= 1
        networks.append(j)
        
    # 초기화
    computers[i][j] = 0
    computers[j][i] = 0

    for nj in range(len(computers)):
        if j != nj and computers[j][nj]:
            computers = dfs(j, nj, networks, computers)
    return computers
```

## 다른 답안 - DFS

```python
def solution(n, computers):
    answer = 0
    visited = [0 for i in range(n)]
    def dfs(computers, visited, start):
        stack = [start]
        while stack:
            j = stack.pop()
            if visited[j] == 0:
                visited[j] = 1
            # for i in range(len(computers)-1, -1, -1):
            for i in range(0, len(computers)):
                if computers[j][i] ==1 and visited[i] == 0:
                    stack.append(i)
    i=0
    while 0 in visited:
        if visited[i] ==0:
            dfs(computers, visited, i)
            answer +=1
        i+=1
    return answer
```

## 다른 답안 - BFS
```python
def solution(n, computers):    
    def BFS(node, visit):
        que = [node]
        visit[node] = 1
        while que:
            v = que.pop(0)
            for i in range(n):
                if computers[v][i] == 1 and visit[i] == 0:
                    visit[i] = 1
                    que.append(i)
        return visit
    visit = [0 for i in range(n)]
    answer = 0
    for i in range(n):
        try:
            visit = BFS(visit.index(0), visit)
            answer += 1
        except:
            break
    return answer
```