## [게임 맵 최단거리](https://programmers.co.kr/learn/courses/30/lessons/1844)

- 문제 설명
bfs 문제의 정석. 게임 맵 (0,0) 좌표에서 (n,m) 좌표까지의 최단거리를 구하는 문제다.

- 입출력 예

|maps|answer|
|-|-|
|[[1,0,1,1,1],[1,0,1,0,1],[1,0,1,1,1],[1,1,1,0,1],[0,0,0,0,1]]|11|
|[[1,0,1,1,1],[1,0,1,0,1],[1,0,1,1,1],[1,1,1,0,0],[0,0,0,0,1]]|-1|


## Answer
특별한 건 없고 bfs 기본문제인 미로찾기와 똑같이 풀었다.
```python
from collections import deque
def solution(maps):

    # 상하좌우
    dx = [0,0,-1,1]
    dy = [-1,1,0,0]

    # init
    n = len(maps)
    m = len(maps[0])
    dist = [[0]*m for _ in range(n)]
    dist[0][0] = 1
    que = deque()
    que.append((0,0))

    # bfs
    while que:
        x, y = que.popleft()

        for i in range(4):
            nx = x + dx[i]
            ny = y + dy[i]

            if 0<=nx<m and 0<=ny<n and not dist[ny][nx]:
                if maps[ny][nx]:
                    dist[ny][nx] = dist[y][x] + 1
                    que.append((nx, ny))

    # 최단거리 반환
    return dist[n-1][m-1] if dist[n-1][m-1] else -1
```