# MST_Prim(최소 비용 신장 트리)

[TOC]

### 알고리즘 코드

```python
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
- 구현 과정에 대한 개념을 아래 간략히 정리해본다.
  - Initialize a tree with a single vertex, chosen arbitrarily from the graph.
  - Grow the tree by one edge: of the edges that connect the tree to vertices not yet in the tree, find the minimum-weight edge, and transfer it to the tree.
  - Repeat step 2 (until all vertices are in the tree).