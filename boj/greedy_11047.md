# 동전 0

전형적인 그리디 문제

## My Answer
```python
from sys import stdin

n, k = map(int, stdin.readline().split())
coins = [int(stdin.readline()) for _ in range(n)]

cnt = 0
for i in reversed(coins):
    if k <= 0:
        break
    if i > k:
        continue
    elif i <= k:
        cnt += k//i
        k %= i

print(cnt)
```

## Shortest Answer
```python
p,*o=open(0)
k=int(p[2:])
c=0
for i in map(int,o[::-1]):c+=k//i;k=k%i
print(c)
```