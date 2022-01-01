# 거리두기 확인하기
구현 문제
- [문제 링크](https://programmers.co.kr/learn/courses/30/lessons/81302?language=python3)
- Lv.2

## My Answer
난이도에 비해 
코드를 너무 지저분하게 짰다 ㅜㅜ 수정 필요
```python
def solution(places):
    result = []
    for room in places:
        isKeep = 1
        for i in range(5):
            for j in range(5):
                if room[i][j] == "P":
                    if not isKeepDistance(room, i, j):
                        isKeep = 0
                        break
        else:
            result.append(isKeep)
    return result

def isKeepDistance(room, y, x):
    # 북서쪽부터 시계 방향
    dx = [-1, 0, 1, 1, 1, 0, -1, -1]
    dy = [-1, -1, -1, 0, 1, 1, 1, 0]

    for i in range(8):
        nx = x + dx[i]
        ny = y + dy[i]
        if 0<nx<5 and 0<ny<5:
            if room[ny][nx] == "P":
                near1_x, near1_y = x + dx[i-1], y + dy[i-1]
                near2_x, near2_y = x + dx[(i+1)%8], y + dy[(i+1)%8]
                if 0<near1_x<5 and 0<near1_y<5:
                    if room[near1_y][near1_x] != "X":
                        return False
                if 0<near2_x<5 and 0<near2_y<5:
                    if room[near2_y][near2_x] != "X":
                        return False

    return True
```