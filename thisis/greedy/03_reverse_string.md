# 문자열 뒤집기

## Shortest Answer
str 클래스의 메소드인 `count`를 이용했다. count는 인자로 받은 문자열이 포함됐는지 확인하고 그 개수를 반환한다.
```python
v=input().count
print((v('10')+v('01')+1)//2)
```

## My Answer
```python
# -*- coding: utf-8 -*-
from sys import stdin
s = stdin.readline().rstrip()

current = s[0]
result = 1
for i in range(1, len(s)):
    if current != s[i]:
        result += 1
        current = s[i]
    
print(result // 2)
```

