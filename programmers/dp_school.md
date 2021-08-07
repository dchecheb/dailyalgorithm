# [등굣길](https://programmers.co.kr/learn/courses/30/lessons/42898)

- 문제 설명<br>
동적계획법 문제. 집에서 학교까지(행렬) 갈 수 있는 최단 경로의 개수를 반환하는 문제다.

- 입출력 예<br>

|m|n|puddles|return|
|-|-|-|-|
|4|3|[[2, 2]]|4|

## My Answer
bfs로 우측, 하단을 bfs로 탐색하고, 현재 위치가 [m,n] 좌표일 때 최솟값을 갱신하고 경로 수를 더해주는 방식이다.
정확성은 테스트 8만 시간초과고, 효율성은 0점 나왔다.
```python
from collections import deque

def solution(m, n, puddles):

    # 학교 가는 길 그래프
    graph = [[10000]*m for _ in range(n)]
    for pm, pn in puddles:
        graph[pn-1][pm-1] = 0

    # bfs
    que = deque()
    que.append((0,0,1))
    graph[0][0] = 1
    minDist = 10000
    cnt = 0

    while que:

        x, y, dist = que.popleft()

        # 현재 좌표가 학교인지 확인
        if x == m-1 and y == n-1:
            if minDist > dist:
                cnt = 1
                minDist = dist
            elif minDist == dist:
                cnt += 1

        # 우측 이동
        nx = x + 1
        if 0 <= nx < m:
            if graph[y][nx]:
                if graph[y][nx] >=  dist+1:
                    graph[y][nx] = dist+1
                    que.append((nx, y, dist+1))
        
        # 하단 이동
        ny = y + 1
        if 0 <= ny < n:
            if graph[ny][x]:
                if graph[ny][x] >= dist+1:
                    graph[ny][x] = dist+1
                    que.append((x, ny, dist+1))

    return cnt%1000000007
```

## Answer
동적 계획법으로 풀어야 하는 문제다. 길은 우측, 하단으로 한 칸씩만 움직일 수 있기 때문에 
어떤 좌표더라도 현재 위치까지 경로의 개수는 좌측, 상단 좌표까지의 경로 개수를 합치면 된다.
```python
def solution(m,n,puddles):
    answer = [[0]*(m+1) for _ in range(n+1)]
    answer[1][1] = 1


    for i in range(1, n+1):
        for j in range(1, m+1):

            # 시작점 pass
            if i == 1 and j == 1:
                continue

            # 동적 계획법 : 상, 좌측 좌표까지의 경로 개수를 합치면 됨
            if [j,i] in puddles:
                answer[i][j] = 0
            else:
                answer[i][j] = answer[i-1][j] + answer[i][j-1]

    return answer[n][m]%1000000007
```

## Reference
- https://codedrive.tistory.com/57