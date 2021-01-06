# swea

# 최소 신장 트리

### 일자 20201107

#### 문제

그래프에서 사이클을 제거하고 모든 노드를 포함하는 트리를 구성할 때, 가중치의 합이 최소가 되도록 만든 경우를 최소신장트리라고 한다.

0번부터 V번까지의 노드와 E개의 간선을 가진 그래프 정보가 주어질 때, 이 그래프로부터 최소신장트리를 구성하는 간선의 가중치를 모두 더해 출력하는 프로그램을 만드시오.


**[입력]**

첫 줄에 테스트 케이스의 개수 T가 주어지고, 테스트 케이스 별로 첫 줄에 마지막 노드번호 V와 간선의 개수 E가 주어진다.

다음 줄부터 E개의 줄에 걸쳐 간선의 양 끝 노드 n1, n2, 가중치 w가 차례로 주어진다. 

1<=T<=50, 1<=V<=1000, 1<=w<=10, 1<=E<=1000000

**[출력]**

각 줄마다 "#T" (T는 테스트 케이스 번호)를 출력한 뒤, 답을 출력한다.



#### 풀이1

```python
def make_set(x):
    p[x] = x

def find_set(x):
    if p[x] != x:
        p[x] = find_set(p[x])
    return p[x]

def union(x, y):
    p[find_set(y)] = find_set(x)


for tc in range(1, int(input())+1):
    V, E = map(int,input().split())
    edges = [list(map(int,input().split())) for _ in range(E)]
    p = [0]*(V+1)
    edges.sort(key=lambda x:x[2])
    # print(edges)
    for i in range(V+1):
        make_set(i)
    # print(p)
    ans = 0
    for i in range(E):
        if find_set(edges[i][0]) != find_set(edges[i][1]):
            union(edges[i][0], edges[i][1])
            ans += edges[i][2]
    print("#{} {}".format(tc, ans))
```

- find_set과 union 알고리즘을 이용한 풀이법

#### 풀이2

```python
def MST_Prim():
    INF = 0xffffff
    key = [INF]*(V+1)
    key[0] = 0


    for _ in range(V+1):
        min_idx = -1
        min_value = INF

        for i in range(V+1):
            if key[i] < min_value and not visit[i]:
                min_value = key[i]; min_idx = i
        visit[min_idx] = True

        for j in range(V+1):
            if not visit[j] and adj[min_idx][j] != 0 and key[j] > adj[min_idx][j]:
                key[j] = adj[min_idx][j]
    return sum(key)

for tc in range(1, int(input())+1):
    V, E = map(int,input().split())
    adj = [[0]*(V+1) for _ in range(V+1)]
    visit = [False]*(V+1)

    for _ in range(E):
        a,b,w = map(int,input().split())
        adj[a][b] = adj[b][a] = w
    # for row in adj:
    #     print(row)
    # print()
    print("#{} {}".format(tc, MST_Prim()))
```

- MST_Prim 알고리즘을 이용한 풀이법

#### 풀이3

```python
import heapq
def MST_Prim():
    visit = [False]*(V+1)
    ans = 0

    heap = []
    heapq.heappush(heap, (0,0))
    visit[0] = True

    while heap:
        w, v = heapq.heappop(heap)

        for new_w, new_v in adj[v]:
            if not visit[new_v]:
                visit[new_v] = True
                heapq.heappush(heap, (new_w, new_v))
                heap.sort()
    return ans


for tc in range(1,int(input())+1):
    V, E = map(int,input().split())
    adj = [[] for _ in range(V+1)]
    for _ in range(E):
        a,b,w = map(int,input().split())
        adj[a].append((w,b))
        adj[b].append((w,a))

    print("#{} {}".format(tc, MST_Prim()))
```

- heap 라이브러리를 이용한 풀이법.
- 위 세가지 방식으로 문제를 다 풀어보았다.