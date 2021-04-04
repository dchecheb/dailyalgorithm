# 곱하기 혹은 더하기

## Book Answer
```python
# -*- coding: utf-8 -*-
data = input()

# 첫 번째 문자를 숫자로 변경하여 대입
result = int(data[0])

for i in range(1, len(data)):
    # 두 수 중 하나라도 '0' or '1'인 경우, 더하기
    num = int(data[i])
    if num <= 1 or result <= 1:
        result += num
    else:
        result *= num
print(num)
```

## My Answer
```python
from sys import stdin
s = [int(i) for i in stdin.readline().rstrip()]

result = 0
for i in s:
    if i <= 1 or result <= 1: 
        result += i
    else:
        result *= i
        
print(result)
```


