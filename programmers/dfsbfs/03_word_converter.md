# [단어 변환](https://programmers.co.kr/learn/courses/30/lessons/43163)

## My Answer
bfs 를 이용하면 목적 노드에 도착했다면 항상 최단 경로임을 보장한다.
begin에서 시작하여 converting 할 수 있는 단어는 queue에 넣는 식으로 너비 우선 탐색을 구현했다.
다른 풀이를 보니 `isConvertable` 에서 `zip` 함수를 사용하는 게 더 pythonic 해보인다.

```python
from collections import deque

def solution(begin, target, words):
    queue = deque()
    queue.append((begin, 0))
    
    while(queue):
        srcWord, depth = queue.popleft()
        if depth > len(words): return 0
        if srcWord == target: return depth
        
        for w in words:
            if isConvertable(srcWord, w):
                queue.append((w, depth + 1))
                
    return 0
              
def isConvertable(src, dst):
    diffCnt = 0
    for i in range(len(src)):
        if src[i] != dst[i]: diffCnt += 1
        if diffCnt > 1: return False
    return True
```