# MST_Prim(최소 비용 신장 트리)

[TOC]

### 알고리즘 코드

```python
'''
3 3
1 2 1
2 3 2
1 3 3
'''
V, E = map(int, input().split())

arr = [[0]*V for _ in range(V)]

for i in range(E):
    a,b,c = map(int, input().split())
    arr[a][b] = c
    arr[b][a] = c

INF = 0xfffff
key = [INF]*V
mst = [False]*V

key[0] = 0
result = 0

cnt = 0

while False in mst:
    minV = INF
    minIdx = 0

    for i in range(V):
        if key[i] < minV and not mst[i]:
            minV = key[i]
            minIdx = i

    mst[minIdx] = True
    result += minV
    cnt += 1
    for w in range(V):
        if arr[minIdx][w] > 0 and arr[minIdx][w] < key[w] and not mst[w]:
            key[w] = arr[minIdx][w]

print(key)
print(result)
```

- **Prim 알고리즘**: 시작 정점에서부터 출발하여 신장트리 집합을 단계적으로 확장해나가는 방법
- Prim 알고리즘의 동작
  - 시작 단계에서는 시작 정점만이 MST(최소 스패닝 트리) 집합에 포함된다.
  - 앞 단계에서 만들어진 MST 집합에 인접한 정점들 중에서 최소 간선으로 연결된 정점을 선택하여 트리를 확장한다.
    즉, 가장 낮은 가중치를 먼저 선택한다.
  - 위의 과정을 트리가 (N-1)개의 간선을 가질 때까지 반복한다.
- 구현 과정에 대한 개념을 아래 간략히 정리해본다.
  - Initialize a tree with a single vertex, chosen arbitrarily from the graph.
  - Grow the tree by one edge: of the edges that connect the tree to vertices not yet in the tree, find the minimum-weight edge, and transfer it to the tree.
  - Repeat step 2 (until all vertices are in the tree).
- Prim 알고리즘의 시간 복잡도
  - 주 반복문이 정점의 수 n만큼 반복하고, 내부 반복문이 n번 반복
    - Prim의 알고리즘의 시간 복잡도는 O(n^2) 이 된다.