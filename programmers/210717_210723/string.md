# [짝지어 제거하기](https://programmers.co.kr/learn/courses/30/lessons/12973)
## Try
문자열을 그대로 받아 string이 사라질 때까지 계속 반복문을 돌렸다.
문자열 길이가 1,000,000인 경우도 있어서 시간초과가 발생했다.
최악의 경우, O(N^2)인 알고리즘이라 발생한 문제다.
```python
def solution(s):
    while s:
        for i in range(len(s)-1):
            if s[i] == s[i+1]:
                s = s[:i] + s[i+2:]
                break
        else:
            return 0
    return 1
```
## Answer
list로 stack을 구현해서 해결했다.
문자열을 한 바퀴만 돌면서 stack의 맨마지막 문자와 stack에 append 하려는 문자열이 일치하는지만 확인하는 방식으로 시간복잡도를 O(N)으로 단축했다.
```python
def solution(s): 
    stack = []

    for i in s:

        # 처음
        if len(stack) == 0: 
            stack.append(i)

        # 마지막 문자열과 비교
        elif stack[-1] == i: 
            stack.pop()

        # 짝이 아닌 경우
        else: 
            stack.append(i)
    
    if len(stack) == 0: 
        return 1
    else: 
        return 0 
```