# [행렬 테두리 회전하기](https://programmers.co.kr/learn/courses/30/lessons/77485)

## Answer
당연히 x가 열이고 y가 행일줄 알고 풀다가 헷갈려서 엄청 오래걸렸다..
계속 이상하게 돌아가서 확인해봤더니 문제를 잘못 읽은 거였다.
다 바꾸긴 힘들어서 결국 `rotate` 메소드에서는 x랑 y랑 바꿔서 풀었다.
```python
def solution(rows, columns, queries):
    
    # Init
    answer = list()
    matrix = list()
    for r in range(rows):
        matrix.append([r*columns + c for c in range(1, columns+1)])
    

    # 회전
    for x1, y1, x2, y2 in queries:
        matrix, minist = rotate(matrix, min(y1, y2)-1, min(x1, x2)-1, max(y2, y1)-1, max(x1,x2)-1)
        answer.append(minist)

    return answer


def rotate(matrix, x1, y1, x2, y2):
    '''
    회전할 테두리의 좌측 상단, 우측 하단 좌표를 인수로 받고
    행렬을 회전 시킨 후 반환
    '''
    dx = x2 - x1
    dy = y2 - y1
    minist = 10000

    # 북 테두리
    srcValue = matrix[y1][x1]       # 원본 위치 값
    for i in range(1, dx+1):
        dstValue = matrix[y1][x1+i]   # 목적지 위치 값
        matrix[y1][x1+i] = srcValue
        srcValue = dstValue

        # 최솟값 갱신
        minist = min(minist, srcValue)

    # 동 테두리
    for i in range(1, dy+1):
        dstValue = matrix[y1+i][x2]
        matrix[y1+i][x2] = srcValue
        srcValue = dstValue

        # 최솟값 갱신
        minist = min(minist, srcValue)

    # 남 테두리
    for i in range(1, dx+1):
        dstValue = matrix[y2][x2-i]
        matrix[y2][x2-i] = srcValue
        srcValue = dstValue

        # 최솟값 갱신
        minist = min(minist, srcValue)
    
    # 서 테두리
    for i in range(1, dy+1):
        dstValue = matrix[y2-i][x1]
        matrix[y2-i][x1] = srcValue
        srcValue = dstValue

        # 최솟값 갱신
        minist = min(minist, srcValue)

    return matrix, minist
```
