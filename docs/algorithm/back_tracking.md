# 백트래킹

제약 조건 만족 문제에서 해를 찾기 위한 전략.
트리 구조를 기반으로 DFS 깊이 탐색을 진행하면서 각 루트에 대해 조건에 부합하는지 체크(Promising)하고, 해당 트리에서 조건에 맞지 않는 노드는 더이상 깊이 탐색을 하지 않고 가지를 쳐버린다.(Prugning)

## 대표 문제 : N-Queen
https://www.acmicpc.net/problem/9663


## Reference
- https://www.fun-coding.org/Chapter21-backtracking-live.html