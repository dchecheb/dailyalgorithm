# [추석트래픽](https://programmers.co.kr/learn/courses/30/lessons/17676)
## My Answer
정확성도 하나 나가고 효율성도 나갔다.. 
ms 단위로 완전 탐색을 해서 최대 처리량을 갱신하는 방식의 풀이다.
```python
from datetime import datetime, timedelta

def solution(lines):
    workTimes = list()
    startTime = datetime.max

    # 시간 문자열 정리
    for line in lines:

        # 문자열 분리
        dateStr, timeStr, workedSec = line.split()
        dateStr += " " + timeStr
        workedSec = float(workedSec[:-1])*1000000

        # time 객체로 변환 후 시작, 종료 시간 저장
        timeObj = datetime.strptime(dateStr, "%Y-%m-%d %H:%M:%S.%f")
        curStartTime = timeObj - timedelta(microseconds=workedSec)
        workTimes.append((curStartTime, timeObj))

        # 전체 시작 시간 갱신
        startTime = min(startTime, curStartTime)


    # 완전탐색
    maxThroughput = 0
    endTime = datetime.min
    while endTime <= workTimes[-1][1]:
        endTime = startTime + timedelta(microseconds=999000)   # 1초 후
        throughput = 0
        for curStartTime, curEndTime in workTimes:
            if curEndTime < startTime or curStartTime > endTime:
                continue
            else:
                throughput += 1
        maxThroughput = max(maxThroughput, throughput)
        startTime += timedelta(microseconds=1000)

    return maxThroughput
```

## Answer
```python
from datetime import datetime, timedelta

def solution(lines):
    if len(lines) == 1:
        return 1
    start_time = []
    time = []
    for i in lines:
        split = i.split(' ')
        mili = int(round(float(split[2][:-1]),3)*1000 -1)
        end = datetime.strptime(split[0]+' ' + split[1], "%Y-%m-%d %H:%M:%S.%f")
        start = end - timedelta(milliseconds=mili)
        start_time.append((start,end)) #lines의 원소의 시작시간과 끝시간을 담아준다.
        time.append(start) # 트래픽이 시작하는 시간을 따로 담아주자.
        time.append(end)
    # start_time = sorted(start_time, key = lambda x : (x[0]))

    i = 0
    result = []
    while i != len(time):
        stand_start = time[i] #트레픽 체크 시작하는 지점
        stand_end = stand_start + timedelta(milliseconds=999) #트레픽 체크가 끝나는 지점
        answer = 0
        for a in start_time:
            if a[0]<=stand_start and a[1]>=stand_start: #끝나는 부분이 트래픽에 포함된 경우
                answer += 1
            elif a[0] <= stand_end and a[1] >= stand_end: #시작하는 부분이 트래픽에 포함된 경우
                answer += 1
            elif a[0] >= stand_start and a[1] <= stand_end: # 전체 구간이 트래픽 구간에 포함되는 경우
                answer += 1

        result.append(answer)
        i += 1
    return max(result)
```