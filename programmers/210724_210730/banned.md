# [불량 사용자](https://programmers.co.kr/learn/courses/30/lessons/64064)

## My Answer
```python
def solution(user_id, banned_id):

    combs = list()
    for _ in user_id:
        uids = user_id[:] # 얕은 복사
        comb = set()

        for bid in banned_id:
            # uid와 비교
            for i in range(len(uids)):
                if check(uids[i], bid):
                    comb.add(uids[i])
                    uids[i] = ""
                    break
            
        # 없다면 경우의 수 추가
        if not comb in combs:
            combs.append(comb)

    return len(combs)

def check(uid, bid):
    '''
    uid가 제재 id인지 확인
    '''
    if len(uid) != len(bid):
        return False

    for u, b in zip(uid, bid):
        if u != b and b != "*":
            return False
    
    return True

u = ["frodo", "fradi", "crodo", "abc123", "frodoc"]
b = ["fr*d*", "abc1**"]  
print(solution(u, b))
```