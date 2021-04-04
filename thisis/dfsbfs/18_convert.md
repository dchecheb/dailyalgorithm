
# Answer
```python
# u 끝자리 index 반환
def balanced_index(p):
    cnt = 0 # 왼쪽 괄호 개수
    for i in range(len(p)):
        if p[i] == "(":
            cnt += 1
        else:
            cnt -= 1
        if cnt == 0:
            return i


# 올바른 괄호 문자열인지 판단
def check_proper(p):
    cnt = 0
    for i in p:
        if i == "(":
            cnt += 1
        else:
            # 문자열 마지막까지 탐색하기 전에 cnt가 0이 됐을 때
            if cnt == 0:
                return False
            cnt -= 1
    return True

def solution(p):
    answer = ''
    if p == '':
        return answer
    index = balanced_index(p)
    u = p[:index + 1]
    v = p[index + 1:]

    # u가 올바른 괄호 문자열이라면 v마저 확인
    if check_proper(u):
        answer = u + solution(v)

    # u가 올바른 괄호 문자열이 아니라면
    else:
        answer = "("
        answer += solution(v)
        answer += ")"
        u = list(u[1:-1])
        for i in range(len(u)):
            if u[i] == "(":
                u[i] = ")"
            else:
                u[i] = "("
        answer += "".join(u)
    return answer

print(solution(")("))
```