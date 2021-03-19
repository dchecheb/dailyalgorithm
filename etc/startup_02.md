## 사은품 교환하기
- [스코페 모의 테스트 문제](https://scofe2021.goorm.io/exam/111379/%EB%AA%A8%EC%9D%98%ED%85%8C%EC%8A%A4%ED%8A%B8-startup-coding-festival-2021/quiz/2)
어렵게 출제한 문제는 아니였는데 처음 생각하는 방향 자체가 꼬여서 풀기 힘들었던 문제다.


### Try
시간 초과가 난 풀이다. 
한 단계씩 판단해가면서 쿠폰의 개수를 삭제하는 식으로 했더니 
n이나 m이 큰 숫장일 수록 시간이 오래걸렸다.

시간초과 뿐 아니라 fail난 테스트케이스도 있었는데 아직 원인은 못찾았다.
```python
# -*- coding: utf-8 -*-
# UTF-8 encoding when using korean
t = int(input())
cases = [list(map(int, input().split())) for _ in range(t)]

for n, m in cases:
    # 음료수를 한 잔도 얻을 수 없을 때
    if n < 5 or m < (12-n):
        print(0)
        continue

    # 최대 상품 수 계산
    cnt = 0
    while n > 0:
        if n >= 5 and m >= 7:
            n -= 5
            m -= 7
            cnt += 1
            continue
        elif n >= 5 and m < 7:
            if n >= 12 -m:
                n -= (12 -m)
                cnt += 1
                continue
            else:
                break
        else:
            break
    print(cnt)
```

## Answer
결국 다른 풀이를 참고했다.
한세트씩 고려하며 count 해나가는 방식 이 아니라,
n / 5 의 결과과 n+m / 12 의 결과 중 작은 것을 선택하는 방식이다.
```python
# -*- coding: utf-8 -*-
# UTF-8 encoding when using korean
t = int(input())
cases = [list(map(int, input().split())) for _ in range(t)]

for n, m in cases:
    k1 = n // 5
    k2 = (n+m) // 12
    k = k1 if k1<k2 else k2
    while n+m < 12*k:
        if k == 0:
            break
        k -= 1
    print(k)
```

## 참조
- https://medium.com/@pjuyeon25/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EC%82%AC%EC%9D%80%ED%92%88-%EA%B5%90%ED%99%98%ED%95%98%EA%B8%B0-2cbd59f474af