# 다단계 칫솔


## My Answer
부모 노드 방향으로 올라가며 돈을 나누어 방식으로 풀었다.
나눌 돈이 1원 미만이거나 루트 노트까지 갔다면 while문을 빠져나간다.

그런데 시간 초과가 난다!
```python
def solution(enroll, referral, seller, amount):
    enroll.append("-")
    earnList = [0]*(len(enroll))   

    for index, child in enumerate(seller):
        money = amount[index] * 100
        earnList[enroll.index(child)] += money

        # 부모 방향으로 위치 이동
        while child != "-" and money > 0:
            parent = referral[enroll.index(child)]

            share = money // 10
            if share < 1:
                share = 0
            earnList[enroll.index(child)] -= share
            earnList[enroll.index(parent)] += share 
            
            # 상향
            child = parent
            money = share

    return earnList
```

## Answer
- [참고](https://velog.io/@qweadzs/%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%A8%B8%EC%8A%A4-%EB%8B%A4%EB%8B%A8%EA%B3%84-%EC%B9%AB%EC%86%94-%ED%8C%90%EB%A7%A4Python)
```python
def find(parents, money, number, answer):
    # 민호까지 돈이 들어오거나 줄 돈이 없으면 종료
    if parents[number] == number or money // 10 == 0:
        answer[number] += money
        return
    send = money // 10
    mine = money - send
    answer[number] += mine
    find(parents, send, parents[number], answer)
    return


def solution(enroll, referral, seller, amount):
    n = len(enroll)  # 총 사람 수(민호 포함 X)
    answer = [0] * (n + 1)  # 민호 포함
    d = {}  # 이름-번호의 key-value를 가지는 딕셔너리
    parents = [i for i in range(n + 1)]  # 각자 자신을 부모로 초기화
    # 이름-번호로 딕셔너리에 저장
    for i in range(n):
        d[enroll[i]] = i + 1
    # 추천인 입력
    for i in range(n):
        if referral[i] == "-":  # 민호가 추천인
            parents[i + 1] = 0
        else:
            parents[i + 1] = d[referral[i]]
    # 칫솔 정산
    for i in range(len(seller)):
        find(parents, amount[i] * 100, d[seller[i]], answer)
    return answer[1:]
```

e = ["john", "mary", "edward", "sam", "emily", "jaimie", "tod", "young"]
r = ["-", "-", "mary", "edward", "mary", "mary", "jaimie", "edward"]
s = ["young", "john", "tod", "emily", "mary"]
a = [12, 4, 2, 5, 10]

e = ["john", "mary", "edward", "sam", "emily", "jaimie", "tod", "young"]
r = ["-", "-", "mary", "edward", "mary", "mary", "jaimie", "edward"]
s = ["sam", "emily", "jaimie", "edward"]
a = [2, 3, 5, 4]
print(solution(e,r,s,a))