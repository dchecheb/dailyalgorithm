# 문자열 뒤집기

## My Answer
같은 숫자의 연속을 한 그룹으로 보고 그룹 개수를 셌다. 예를 들어, 001100 이면 00, 11, 00 이렇게 3그룹으로 나뉜다.
0 또는 1로 이루어진 그룹 중 더 개수가 적은 것을 전부 뒤집는으면 모두 같은 숫자로 만들 수 있기 때문에
0의 그룹 개수, 1의 그룹 개수 중 더 적은 것을 답으로 구해지게끔 했다.
0 그룹과 1 그룹의 개수 차이는 1을 넘을 수 없으므로 2로 나눈 몫을 답으로 출력했다.

```python
from sys import stdin

string = [int(i) for i in stdin.readline().rstrip()]

cnt = 1
prev = string[0]
for i in range(1, len(string)):
    if prev != string[i]:
        cnt += 1
    prev = string[i]

print(cnt // 2)
```

## Book Answer

```python
data = input()

```