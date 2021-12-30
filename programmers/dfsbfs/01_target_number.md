## 타겟 넘버

### 문제 설명
n개의 음이 아닌 정수가 있습니다. 이 수를 적절히 더하거나 빼서 타겟 넘버를 만들려고 합니다. 예를 들어 [1, 1, 1, 1, 1]로 숫자 3을 만들려면 다음 다섯 방법을 쓸 수 있습니다.

```
-1+1+1+1+1 = 3
+1-1+1+1+1 = 3
+1+1-1+1+1 = 3
+1+1+1-1+1 = 3
```

사용할 수 있는 숫자가 담긴 배열 numbers, 타겟 넘버 target이 매개변수로 주어질 때 숫자를 적절히 더하고 빼서 타겟 넘버를 만드는 방법의 수를 return 하도록 solution 함수를 작성해주세요.

### 제한사항
주어지는 숫자의 개수는 2개 이상 20개 이하입니다.
각 숫자는 1 이상 50 이하인 자연수입니다.
타겟 넘버는 1 이상 1000 이하인 자연수입니다.

### 입출력 예
|numbers|target|return|
|-|-|-|
|[1, 1, 1, 1, 1]|3|5|

###  My Answer
```python
from itertools import product

def solution(numbers, target):
    optCombs = product(["+", "-"], repeat=len(numbers))
    cnt = 0
    for opts in optCombs:
        result = 0
        for i in range(len(numbers)):
            if opts[i] == "+": result += numbers[i]
            elif opts[i] == "-": result -= numbers[i]
        if result == target: cnt += 1
    return cnt
```

### Other Answer
재귀를 이용한 풀이. 출제 의도에 가장 부합해보임.
```python
def solution(numbers, target):
    if not numbers and target == 0 :
        return 1
    elif not numbers:
        return 0
    else:
        return solution(numbers[1:], target-numbers[0]) + solution(numbers[1:], target+numbers[0])
```

엄청나게 파이써닉한 코드를 풀이를 발견해서 가져왔다.
- `product` : 중복 순열을 구해주는 메소드. iterable 객체의 요소 간 데카르트 곱(cartesian product)를 계산하여 iterator로 반환.
- `map` : iterable 객체의 각 요소를 지정된 함수로 처리해주는 메소드
```python
from itertools import product
def solution(numbers, target):
    l = [(x, -x) for x in numbers]
    s = list(map(sum, product(*l)))
    return s.count(target)
```

- https://programmers.co.kr/learn/courses/30/lessons/43165
