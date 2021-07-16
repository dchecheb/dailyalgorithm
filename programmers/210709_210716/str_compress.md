# [문자열압축](https://programmers.co.kr/learn/courses/30/lessons/60057)

## My Answer
```python
def solution(s):
    if len(s) == 1:
        return 1

    answer = 1000           # 최솟값
    cutNum = 1              # 자르는 단위 수
    while cutNum <= len(s) // 2:

        cnt = 1             # 몇 번째 반복인지 카운트
        repeat = ""         # 반복 체크할 문자열
        result = ""         # 최종 압축 문자열
        for i in range(0, len(s), cutNum):
            if repeat == s[i:i+cutNum]:
                cnt += 1
            else:
                result += repeat if cnt == 1 else str(cnt) + repeat
                repeat = s[i:i+cutNum]
                cnt = 1
        result += repeat if cnt == 1 else str(cnt) + repeat

        # 자르는 단위 수 연장
        cutNum += 1

        # 최솟값 갱신
        answer = min(answer, len(result))

    return answer

string = "aabbaccc"
string = "ababcdcdababcdcd"
# string = "abcabcdede"
# string = "anananana"
# string = "a"
print(solution(string))
```