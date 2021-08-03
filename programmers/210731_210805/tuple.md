# [튜플](https://programmers.co.kr/learn/courses/30/lessons/64065)

- 입출력 예

| s | result |
|-|-|
|"{{2},{2,1},{2,1,3},{2,1,3,4}}"|[2, 1, 3, 4]|
|"{{1,2,3},{2,1},{1,2,4,3},{2}}"|2, 1, 3, 4]|
|"{{20,111},{111}}"|111, 20]|
|"{{123}}"|123]|
|"{{4,2,3},{3},{2,3,4,1},{2,3}}"|3, 2, 4, 1]|

집합 형식으로 주어진 문자열을 튜플로 바꾸는 문제다. 문제를 처음 읽었을 때 어떻게 튜플의 순서까지 도출되는지 이해가 안갔다. 프로그래머스의 질문을 보고 나서 집합에서 가장 **빈번히** 나온 숫자 순서대로 튜플이 구성된다는 것을 알았다.

그새서 list `sort()` 내장 함수의 `key` 파라미터에 `lambda x: nums.count(x)`를 넣어 가장 빈도가 적은 순대로 정렬되도록 하고 다시 뒤집었다.

## Answer

```python
import re
def solution(s):
    nums = list(map(int, re.findall("(\d+)",s)))    # 정규표현식으로 숫자 파싱
    answer = list(set(nums)) # 중복 제거
    answer.sort(key=lambda x: nums.count(x)) # 가장 빈번히 나온 숫자 순으로 정렬
    answer.reverse()

    return answer
```