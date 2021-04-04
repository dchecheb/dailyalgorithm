
## 동적 계획법

### 정의

- 복잡한 문제를 간단한 여러 개의 하위 문제로 나누어 푸는 알고리즘.
- 입력 크기가 작은 부분 문제들을 해결한후, 해당 부분문제의 해를 활용해서 보다 큰 크기의 - 부분 문제를 해결한다. 최종적으로는 전체 문제를 해결한다.

- **memoization**<br>
프로그램 실행 시 이전에 계산한 값을 저장하여, 다시 계산하지 않도록 하여 전체 실행 속도를 빠르게 하는 기술
<br>

### 시간복잡도
O(N)
<br>

### 구현 방식
- top-down(memoization): 중복되는 하위 문제를 결합하여 최종적으로 최적해를 구하는 방식
```python
num = 10
dp = [0 for _ in range(num+1)]
def fibo(n):
    if n <= 1:
        return n
    if dp[n]:
        return dp[n]
    else:
        dp[n] = fibo(n-2) + fibo(n-1)
        return dp[n]
print(fibo(num))
```
- bottom-up: 하위 문제들로 상위 문제의 최적해를 구하는 방식
```python
def fibo_dp(num):
    dp = [0 for _ in range(num+1)]
    dp[0] = 0
    dp[1] = 1
    for index in range(2, num+1):
        dp[index] = dp[index-1] + dp[index-2]
    return dp[num]
print(fibo_dp(10))
```
<br>


## Reference
- https://www.fun-coding.org/Chapter14-dp_divide.html
- https://github.com/JaeYeopHan/Interview_Question_for_Beginner/tree/master/Algorithm
- https://cupjoo.tistory.com/20
- [풀이 요령](http://kmelon55.com/?p=210)
