# 만들 수 없는 금액
아직 이해가 잘 안가는 문제다.
target = 2+2 = 4로 계산됐을 때, 왜 3까지의 모든 금액은 만들 수 있다는 건지 이해가 잘... 안간다.

## Book Answer
```python
from sys import stdin

N = int(stdin.readline())
coins = stdin.readline().split()

target = 1
for c in coins:
    if target < c:
        break
    target += c
print(target)
```