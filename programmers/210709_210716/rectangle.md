# [멀쩡한 사각형](https://programmers.co.kr/learn/courses/30/lessons/62048)

## Answer
대각선으로 잘린 사각형 중 멀쩡한 사각형의 개수를 구하는 문제.
주어진 w,h 값의 최대 공약수를 구하면 된다.
수학적 사고를 요하는 문제였다.

최대 공약수가 1 즉, 서로소일 때는 `w+h-1`이 잘리는 사각형의 개수다.
```python
import math
def solution(w,h):
    return w*h - (w+h-math.gcd(w,h))
```

## Reference
- [코드 참조](https://leedakyeong.tistory.com/entry/%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%A8%B8%EC%8A%A4-%EB%A9%80%EC%A9%A1%ED%95%9C-%EC%82%AC%EA%B0%81%ED%98%95-in-python)