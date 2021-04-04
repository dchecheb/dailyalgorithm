# 모험가 길드

## Book Answer
```python
#coding:utf8
# 모험가 길드 문제 정답

n = int(input())
data = list(map(int,input().split()))
data.sort()

result = 0          # 총 그룹 수
count = 0           # 현재 그룹에 포함된 모험가 수
for i in data:      # 공포도를 낮은 것부터 하나씩 확인하며
    count += 1      # 현재 그룹에 해당 모험가를 포함시키기
    if count >= i:  # 현재 그룹에 포함된 모험가의 수가 현재의 공포도 이상이라면, 그룹 결성
        result += 1 # 총 그룹 수 증가시키기
        count = 0   # 현재 그룹에 포함된 모험가 수 초기화

print(result)
```

## My Answer
```python
#coding:utf8
from sys import stdin
n = int(stdin.readline())   # 모험가 수
data = sorted(list(map(int, stdin.readline().split()))) # 모험가 별 공포도
group = 0 # 그룹 수

index = 0
while index < n:
    afraid = data[index]
    index += afraid # next index
    if index >= n:
        break
    if data[index-1] > afraid:
        break

    group += 1

print(group)
```