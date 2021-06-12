# [타겟넘버](https://programmers.co.kr/learn/courses/30/lessons/43165)

## My Answer
문제 의도가 이게 아닌듯하다. 
dfs 문제니까 [중복 순열](https://velog.io/@dchecheb/python%EC%A1%B0%ED%95%A9-%EC%88%9C%EC%97%B4-%EA%B5%AC%ED%98%84%ED%95%98%EA%B8%B0)을 재귀로 직접 구현하는 게 문제 의도일 것이다! dfs로 꼭 구현해보자!
```python
from itertools import product

def solution(numbers, target):
    opt = {
        "+": lambda x, y: x + y,
        "-": lambda x, y: x - y,
    }
    combs = list(product(opt.keys(), repeat=len(numbers)))
    answer = 0
    for comb in combs:
        result = 0
        for i in range(len(numbers)):
            result = opt[comb[i]](result, numbers[i])
        if result == target:
            answer += 1
    return answer
```

## 다른 정답 - dfs
이건 진짜 미친 사람 같다... 천재 아닐까???
```python
def solution(numbers, target):
    if not numbers and target == 0 :
        return 1
    elif not numbers:
        return 0
    else:
        return solution(numbers[1:], target-numbers[0]) + solution(numbers[1:], target+numbers[0])
```
## 다른 정답 - itertools
굉장히 pythonic 한 코드라 가져와 봤다.
```python
from itertools import product
def solution(numbers, target):
    l = [(x, -x) for x in numbers]
    s = list(map(sum, product(*l)))
    return s.count(target)
```