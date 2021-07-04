# [오픈채팅방](https://programmers.co.kr/learn/courses/30/lessons/42888)
## My Answer
dictionay를 이용해서 uid에 대응하는 닉네임을 항상 key,value 형태로 저장했다.
그리고 기록별로 최종적으로 출력할 uid와 한국어를 결과 리스트에 담아서 uid만 name으로 변환해준 후 반환했다.
```python
def solution(record):
    nameDict = dict()   # {uid: name}
    result = list()     # uid + msg 리스트
    answer = list()     

    # msg 정리
    for msg in record:
        splitedMsg = msg.split()
        if "Enter" == splitedMsg[0]:
            _, uid, name = splitedMsg
            result.append((uid,"님이 들어왔습니다."))
            nameDict[uid] = name
        elif "Leave" == splitedMsg[0]:
            _, uid = splitedMsg
            result.append((uid,"님이 나갔습니다."))
        else:
            _, uid, name = splitedMsg
            nameDict[uid] = name

    # uid에 name 대입
    for uid, msg in result:
        answer.append(nameDict[uid] + msg)

    return answer
```