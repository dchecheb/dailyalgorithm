#coding:utf8
# 동전의 개수가 한정적일 때의 동전문제
# 화폐 단위가 작은 순서대로 동전을 확인하며, 현재 확인하는 동전을 이용해 target 금액 또한 만들 수 있는지 확인한다.
# 항상 현재 상태를 '1부터 target - 1 까지의 모든 금액을 만들 수 있는 상태'라고 가정한다.
from sys import stdin
n = int(stdin.readline())
coins = sorted(list(map(int, stdin.readline().split())))


target = 1  # 매 단게마다 target원을 만들 수 있는지 확인. 처음에는 1원을 만들 수 있는지부터 확인한다.
for x in coins:
    # target보다 x가 더 커지면 target은 만들 수 없는 값이 됨.
    if target < x:
        break
    target += x
print(target)




