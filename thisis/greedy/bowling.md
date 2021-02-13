# 볼링공 고르기

## My Answer
이중 포문으로 전부 돌면서 확인하는 방식.
```python
from sys import stdin

N, M = list(map(int, stdin.readline().split()))
bowls = list(map(int, stdin.readline().split()))
cnt = 0
for i, b in enumerate(bowls):
    for j in range(i+1, N):
        if b != bowls[j]:
            cnt += 1
print(cnt)
```

## Book Answer
무게마다 볼링공이 몇 개 있는지 계산한 후, 무게가 작은 볼링공부터 순서대로 확인한다. 확인 단계마다 무거운 볼링공일 수록 선택지가 줄어들게 한다.

```python
n, m = map(int, input().split())
data = list(map(int, input().split()))

array = [0]*11
for x in data:
    array[x] += 1

result = 0
for i in range(1, m+1):
    n -= array[i] # 무게가 i인 볼링공의 개수(A가 선택할 수 있는 개수 제외)
    result += array[i] * n # B가 선택하는 경우의 수와 곱하기
print(result)
```