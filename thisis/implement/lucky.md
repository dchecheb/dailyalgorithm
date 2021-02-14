## My Answer
```python
from sys import stdin

string = stdin.readline().rstrip()
mid = len(string) // 2

left = 0
for l in string[:mid]:
    left += int(l)
right = 0
for r in string[mid:]:
    right += int(r)

if left == right:
    print("LUCKY")
else:
    print("READY")
```

## Book Answer
