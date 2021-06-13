# 최단 경로 

## 정의
- 두 노드를 잇는 가장 짧은 경로를 찾는 문제
- 가중치 그래프에서 간선의 가중치 합이 최소가 되도록 하는 경로를 찾는다.

## 유형
- **단일 출발 & 단일 도착**
- **단일 출발([다익스트라 알고리즘](#다익스트라-최단경로-알고리즘))** : 하나의 정점에서 다른 모든 정점 간의 각각 짧은 거리를 구하는 문제
- **전체 쌍 최단 경로([플로이드 워셜 알고리즘](#플로이드-워셜-알고리즘))**
  
## 알고리즘 종류
### 다익스트라 최단경로 알고리즘
- 특정 노드에서 출발하여 다른 노드로 가는 각각의 최단 경로를 구해주는 알고리즘
- '음의 간선' 즉, 가중치가 음수인 간선이 없을 때 정상적으로 동작한다.
- 각 노드에 대한 현재까지의 최단 거리 정보를 항상 1차원 리스트에 저장하며 리스트를 계속 갱신한다.

#### 구현
- 간단한 다익스트라 알고리즘

시간 복잡도 : O(V^2)<br>
최단 거리가 가장 짧은 노드를 매번 선형 탐색 + 현재 노드와 연결 노드 확인 -> V^2
```python
import sys
input = sys.stdin.readline
INF = int(1e9) # 10억. 무한을 의미. 

n, m = map(int, input().split()) # 노드 수, 간선 수
start = int(input())             # 시작 번호
graph = [[] for i in range(n+1)] # 연결 정보 담을 그래프
visited = [False]*(n+1)          # 방문 체크
distance = [INF]*(n+1)           # 최단 거리 저장

for _ in range(m):
    a, b, c = map(int, input().split()) # a -> b, c는 가중치
    graph[a].append((b,c))


def get_smallest_node():
    '''
    방문하지 않은 노드 중 가장 최단 거리가 짧은 노드 반환
    '''
    min_value = INF
    index = 0
    for i in range(1, n+1):
        if distance[i] < min_value and not visited[i]:
            min_value = distance[i]
            index = i
    return index

def dijkstra(start):
    '''
    노드별 최단거리 저장
    '''
    # 시작노드 초기화
    distance[start] = 0
    visited[start] = start
    for j in graph[start]:
        distance[j[0]] = j[1]


    # 시작노드 제외한 전체
    for i in range(n-1):
        now = get_smallest_node()
        visited[now] = True
        for j in graph[now]:
            cost = distance[now] + j[1]
            if cost < distance[j[0]]:
                distance[j[0]] = cost

dijkstra(start)

# 모든 노드로 가기 위한 최단 거리 출력
for i in range(1, n+1):
    if distance[i] == INF:
        print("INFINITY")
    else:
        print(distance[i])
```

- 개선된 다익스트라 알고리즘

시간복잡도 : O(ElogV)<br>
최단거리가 가장 짧은 노드를 찾기 위해서 **힙** 자료구조를 사용
```python
import heapq
import sys
input = sys.stdin.readline
INF = int(1e9) # 10억. 무한을 의미. 

n, m = map(int, input().split()) # 노드 수, 간선 수
start = int(input())             # 시작 번호
graph = [[] for i in range(n+1)] # 연결 정보 담을 그래프
distance = [INF]*(n+1)           # 최단 거리 저장

for _ in range(m):
    a, b, c = map(int, input().split()) # a -> b, c는 가중치
    graph[a].append((b,c))

def dijkstra(start):
    que = []
    heapq.heappush(que, (0, start)) # 거리, 노드
    distance[start] = 0
    while que:
        dist, now = heapq.heappop(que)
        # 방문 체크
        if distance[now] < dist:
            continue

        # 인접 노드
        for ad_node, ad_dist in graph[now]:
            cost = dist + ad_dist # 현재 노드까지 거리 + 현재노드에서 인접 노드까지 거리

            # 최솟값 갱신
            if cost < distance[ad_node]:
                distance[ad_node] = cost
                heapq.heappush(que, (cost, ad_node))

dijkstra(start)

# 모든 노드로 가기 위한 최단 거리 출력
for i in range(1, n+1):
    if distance[i] == INF:
        print("INFINITY")
    else:
        print(distance[i])
```

### 플로이드 워셜 알고리즘



## Reference
- https://mattlee.tistory.com/50
- https://www.fun-coding.org/Chapter20-shortest-live.html