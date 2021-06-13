## 힙

### 정의
- 데이터 중 최대값과 최소값을 빠르게 찾기 위해 고안된 **완전이진트리**(노드 삽입 시, 최하단 왼쪽 노드부터 차례대로 삽입하는 크리)
- 우선순위 큐를 구현할 때 사용하기도 한다.

### 시간복잡도
- 일반 배열에서 최대&최소값을 찾을 때 : O(N)
- 힙을 통한 최대&최소값 : O(logN)

### 이진 탐색 트리와의 공통점과 차이점
- 공통점 : 이진 트리다.
- 차이점
    - 힙은 각 노드의 값이 자식 노드보다 크거나 같다.(Max Heap)
    - 이진 탐색 트리는 왼쪽 노드의 값이 가장 작고, 오른쪽 노드 값이 가장 크다.
    - 힙은 왼쪽 자식노드가 오른쪽 자식노드보다 작다는 조건이 없다.
    - 이진 탐색트리는 탐색을 위한 구조, 힙은 최대/최소값을 위한 구조 중 하나라고 이해하면 된다.


### 모듈 사용법
python의 `heapq` 모듈은 최소 힙에 기반한다.
```python
import heapq
heap = list()

# 원소 추가
heapq.heappush(heap, 4)
heapq.heappush(heap, 1)
heapq.heappush(heap, 7)
heapq.heappush(heap, 3) # heap = [1, 3, 7, 4]
```
현재 수 인덱스를 k라 할 때
`2*k + 1`보다 현재 수가 작아야 최소힙 조건에 만족한다.

```python
# 원소 삭제
heapq.heappop(heap) # heap = [3, 4, 7]
```
큐의 최소값을 삭제한다.
```python
# list to heap
heap = [4, 1, 7, 3, 8, 5]
heapq.heapify(heap) # heap = [1, 3, 5, 4, 8, 7]
```

## Reference
- [python 모듈](https://www.daleseo.com/python-heapq/)
- https://www.fun-coding.org/Chapter11-heap.html