## My Answer

```python
p = input()
alpha = ['a','b','c','d','e','f']
x = alpha.index(p[0])
y = int(p[1])

dx = [2,2,1,-1,-2,-2,1,-1]
dy = [1,-1,2,2,1,-1,-2,-2]
cnt = 0
for i in range(8):
    nx = x + dx[i]
    ny = y + dy[i]
    if 0 <= nx <= 7 and 1 <= ny <= 8:
        cnt += 1
print(cnt)
```