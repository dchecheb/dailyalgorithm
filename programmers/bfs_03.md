# [단어 변환](https://programmers.co.kr/learn/courses/30/lessons/43163)
BFS 응용 문제<br>
어찌저찌 풀긴했는데 거의 1시간 가량 걸렸다.<br>
그렇게 난이도 있는 문제였던 것 같진 않았는데.. 나는 좀 디버깅 하는 데 오래 걸리는 편인 것 같다. 연습을 많이 해야겠다!

## My Answer

```python
from collections import deque

def solution(begin, target, words):
    if target not in words:
        return 0

    # 1글자 차이면 인접한다 가정하고 그래프 생성
    graph = dict()
    graph[begin] = list()
    for w in words:
        # begin
        if chkMovable(begin, w):
            graph[begin].append(w)

        # words
        graph[w] = list()
        for w2 in words:
            if chkMovable(w, w2):
                graph[w].append(w2)
    
    # bfs
    minList = [50]*len(words)
    queue = deque()
    queue.append((begin, 0))
    while queue:
        node, cnt = queue.popleft()
        for n in graph[node]:
            if minList[words.index(n)] > cnt+1:
                minList[words.index(n)] = cnt+1
                queue.append((n, cnt+1))

    return minList[words.index(target)]


def chkMovable(src, dst):
    '''
    이동할 수 있는지 체크.
    즉, src가 하나만 바뀌면 dst이 되는지 체크
    '''
    newSrc = src
    cnt = 0
    for i in range(len(src)):
        if cnt > 1: return False
        if src[i] != dst[i]:
            newSrc = src[:i] + dst[i] + src[i+1:]
            cnt += 1
        if newSrc == dst:
            return True if cnt == 1 else False
```

## 다른 정답
python 내장함수 `zip`을 쓰는 아주 간단한 방법이 있었다!
`zip()`은 인수로 받은 두 iterable한 객체를 순서대로 조합하여 리턴해준다. 이걸 이용하면 문자열을 쉽게 비교할 수 있다.
```python
from collections import deque


def get_adjacent(current, words):
    for word in words:
        if len(current) != len(word):
            continue

        count = 0
        for c, w in zip(current, word):
            if c != w:
                count += 1

        if count == 1:
            yield word


def solution(begin, target, words):
    dist = {begin: 0}
    queue = deque([begin])

    while queue:
        current = queue.popleft()

        for next_word in get_adjacent(current, words):
            if next_word not in dist:
                dist[next_word] = dist[current] + 1
                queue.append(next_word)

    return dist.get(target, 0)

```