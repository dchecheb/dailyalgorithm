# 효율성

## 파이썬 시간복잡도
2020년 파이썬 3.7 기준으로 코드를 작성할 때, 자신의 코드가 1초에 2,000만번의 연산을 수행한다고 가정하고 문제를 풀면 시간 제한에 보통 문제가 없다.


## 파이썬에서 리스트 크기
대체로 코딩 테스트에서는 128~512MB로 메모리를 제한한다. 가끔 메모리 제한이 있음에도 수백만 개 이상의 데이터를 처리해야하는 문제가 있을 수도 있으므로 메모리 제한을 꼭 염두에 두어야 한다.
코테 알고리즘에서는 보통 int 자료형을 담은 리스트를 사용한다. 

| 리스트 길이(데이터 개수) | 메모리 사용량 |
| :-----------------:| :---------: |
| 1,000 | 약 4KB |
| 1,000,000 | 약 4MB |
| 1,0,000,000 | 약 40MB |

리스트 크기가 1,000만 이상인 리스트가 있다면 메모리 용량 제한으로 문제를 풀 수 없을 수도 있다.
