# 무지의 먹방 라이브

## My Answer
k초까지 while문을 돌린다.
i(단계)를 이용하여 index를 계산하고 섭취 여부를 판단한다.

#### 단계마다 아래 과정을 거친다.
- i을 1 증가 시킨다. -> 몇 번째 단계인지 나타냄. index를 구하기 위함
- `food_times[index]`가 0보다 크다면 1을 감소시키고 cnt를 올린다. -> 음식을 섭취하고 k초가 지난 것.
- 0보다 작다면 continue -> 접시에 음식이 없어서 넘긴 것.

```python
def solution(food_times, k):
    cnt = 0
    i = -1
    while cnt <= k:
        i += 1
        index = i % len(food_times) # index를 구하기 위해 나머지 사용

        # k초가 됐을 때 먹어야 할 음식 return 
        if cnt == k:
            if food_times[index] > 0:
                return index + 1
            else:
                return -1

        # k초 전까지 계속 섭취
        if food_times[index] > 0:
            cnt += 1
            food_times[index] -= 1
        else:
            continue
```

## Book Answer
전반적으로 그리디 문제의 모범 답안은 정렬한 후 단계마다 확인하는 식의 풀이과정이 많다. 나는 그리디보다는 완탐 방식으로 많이 풀어왔던 것 같다. 그리디는 정말 많이 풀어봐야겠다.

우선순위 큐를 이용했다.
```python
```
