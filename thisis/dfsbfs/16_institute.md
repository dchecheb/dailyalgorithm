
## Answer
```python
from sys import stdin

n, m = map(int, stdin.readline().split())
data = []
temp = [[0]*m for _ in range(n)]
for _ in range(n):
    data.append(list(map(int, stdin.readline().split())))

dx = [-1,0,1,0]
dy = [0,1,0,-1]

result = 0

# dfs로 빈칸인 곳에 전염시킴
def virus(x, y):
    for i in range(4):
        nx = x + dx[i]
        ny = y + dy[i]
        if nx >= 0 and nx < n and ny >= 0 and ny < m:
            if temp[nx][ny] == 0:
                temp[nx][ny] = 2
                virus(nx, ny)

# 안전 영역 크기 계산
def get_score():
    score = 0
    for i in range(n):
        for j in range(m):
            if temp[i][j] == 0:
                score += 1
    return score

def dfs(cnt):
    global result

    if cnt == 3:
        for i in range(n):
            for j in range(m):
                temp[i][j] = data[i][j]
        for i in range(n):
            for j in range(m):
                if temp[i][j] == 2:
                    virus(i,j)
        
        # 안전 영역의 최댓값 계산
        result = max(result, get_score())
        return

    for i in range(n):
        for j in range(m):
            if data[i][j] == 0:
                data[i][j] = 1
                cnt += 1
                dfs(cnt)
                data[i][j] = 0
                cnt -= 1

```