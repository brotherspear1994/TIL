# Dijkstra

[TOC]

### 알고리즘 코드

```python
V, E = map(int,input().split())
adj = {i:[] for i in range(V)}
for i in range(E):
    n1,n2,c = map(int,input().split())  #시작정점,끝정점,가중치
    adj[n1].append([n2,c])  #도착정점, 가중치
print(adj)
INF = 999999    #큰값
dist = [INF] * V    #각정점의 최단거리(현재까지의)
selected = [False] * V
#시작점 : 0번에서 시작
dist[0] = 0
cnt = 0
while cnt <= V-1:
    #최소값 찾기
    minV = INF
    u = -1
    for i in range(V):
        #아직 최단거리가 결정 안되고, 최소인 정점을 선택
        if not selected[i] and minV > dist[i]:
            minV = dist[i]
            u = i
    selected[u] = True
    cnt+=1
    #간선완화
    for w,cost in adj[u]:       #도착정점, 가중치
        if dist[w] > dist[u] + cost:
            dist[w] = dist[u] + cost
print(dist)
```

- **Prim 알고리즘**: **Dijkstra's** algorithm (or **Dijkstra's** Shortest Path First algorithm, SPF algorithm) is an algorithm for finding the shortest paths between nodes in a graph, which may represent, for example, road networks. It was conceived by computer scientist Edsger W. **Dijkstra** in 1956 and published three years later.
- 구현 과정을 아래 간략히 정리해본다.
  - 출발점으로부터의 최단거리를 저장할 배열 d[v]를 만들고, 출발 노드에는 0을, 출발점을 제외한 다른 노드들에는 매우 큰 값 INF를 채워 넣는다. (정말 무한이 아닌, *무한으로 간주될 수 있는 값*을 의미한다.) 보통은 최단거리 저장 배열의 이론상 최대값에 맞게 INF를 정한다. 실무에서는 보통 d의 원소 타입에 대한 최대값으로 설정하는 편.
  - 현재 노드를 나타내는 변수 A에 출발 노드의 번호를 저장.
  - A로부터 갈 수 있는 임의의 노드 B에 대해, d[A] + P(A)(B)와 d(B)의 값을 비교한다. INF와 비교할 경우 무조건 전자가 작다
  - 만약 d[A] + P(A)(B)의 값이 더 작다면, 즉 더 짧은 경로라면, d[B]의 값을 이 값으로 갱신시킨다.
  - A의 모든 이웃 노드 B에 대해 이 작업을 수행한다.
  - A의 상태를 "방문 완료"로 바꾼다. 그러면 이제 더 이상 A는 사용하지 않는다.
  - "미방문" 상태인 모든 노드들 중, 출발점으로부터의 거리가 제일 짧은 노드 하나를 골라서 그 노드를 A에 저장한다.
  - 도착 노드가 "방문 완료" 상태가 되거나, 혹은 더 이상 미방문 상태의 노드를 선택할 수 없을 때까지, 3~7의 과정을 반복한다.

----------------------------------

- 다익스트라 개념 정리

  - **하나의 시작 정점**으로부터 **모든 다른 정점까지의 최단 경로를 찾는 알고리즘**이다.

- MST Prim vs Dijkstra

  - 프림은 다익스트라와 달리 두 노드 사이가 최단거리가 아닐 수도 있다.

    ※ 프림은 1->3의 비용이 3인 반면에, 다익스트라는 1->3의 비용이 2이다.

  - 프림은 무향 그래프에서만 작동하고, 다익스트라는 무향, 유향 그래프에서 모두 작동한다.

  - 프림이 다익스트라를, 다익스트라가 프림을 보장해주지 않는다.

      -> 최소스패닝트리가 최단경로트리를, 최단경로트리가 최소스패닝트리를 보장하지 않는다.

  