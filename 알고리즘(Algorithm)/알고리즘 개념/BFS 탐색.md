# BFS 탐색

[TOC]

### BFS 탐색 알고리즘 1

```python
'''
7 8
1 2 1 3 2 4 2 5 4 6 5 6 6 7 3 7
'''
def bfs(v):
    # 큐, 방문
    Q = []
    visit = [0] * (V+1)

    # enQ(v), visit(v)
    Q.append(v)
    visit[v] = 1
    print(v, end=' ')
    # 큐가 비어있지 않은 동안
    while Q:
        # v = deQ()
        v = Q.pop(0)
        # v의 인접한 정점(w), 방문안한 정점이면
        for w in range(1,V+1):
            if G[v][w] == 1 and visit[w] == 0:
                Q.append(w)
                visit[w] = 1
                print(w, end=' ')
            # enQ(w), 방문처리(w)

# 입력 -> 인접행렬
V, E = map(int,input().split())
temp = list(map(int,input().split()))
G = [[0] * (V+1) for _ in range(V+1)]
for i in range(E):
    s, e = temp[2*i], temp[2*i+1]
    G[s][e] = G[e][s] = 1
# 인접행렬 출력하기.
for i in range(1,V+1):
    print("{} {}".format(i,G[i]))
bfs(1)
```



### BFS 탐색 알고리즘 2

```python
# 입력 -> 인접리스트

def bfs(v):
    global visit
    Q = []
    Q.append(v)
    visit[v] = 1
    print(v, end=' ')
    while Q:
        v = Q.pop(0)
        for w in G[v]:
            if not visit[w]:
                Q.append(w)
                visit[w] = visit[v]+1
                print(w, end= ' ')

V, E = map(int,input().split())
temp = list(map(int,input().split()))
# 인접 리스트
G = [[] for _ in range(V+1)]
# print(G)
visit = [0] * (V+1)
for i in range(E):
    s, e = temp[2*i], temp[2*i+1]
    G[s].append(e)
    G[e].append(s)
print(G)
bfs(1)
maxI = 0
for i in range(1, V+1):
    if visit[maxI] < visit[i]:
        maxI=i
print()
print(maxI, visit[maxI]-1)

########################################################

def bfs(v):
    global visit
    Q = []
    Q.append(v)
    visit[v] = 1
    print(v, end= ' ')
    while Q:
        v = Q.pop()
        for w in G[v]:
            if not visit[w]:
                Q.append(w)
                visit[w] = visit[v] + 1
                print(w, end= ' ')

V, E = map(int,input().split())
temp = list(map(int,input().split()))
G = [[] for _ in range(V+1)]
for i in range(E):
    s, e = temp[i*2], temp[i*2+1]
    G[s].append(e)
    G[e].append(s)
# print(G)
visit = [0]*(V+1)
bfs(1)
print()
maxI = 0
for i in range(1,V+1):
    if visit[maxI] < visit[i]:
        maxI = i
dis = maxI - 1
print("출발 간선과의 정류장 번호와 거리 차이는 : {} {}".format(dis, visit[maxI]))
```

- 깊이 우선탐색(DFS)에 이어 어느정도 DFS가 익숙해졌을 때쯤, 너비우선탐색(BFS)를 학습한 기억이 난다.
- 위는 BFS 알고리즘을 처음 학습했을 당시의 코드이다.
- 당시 학습을 하며, `DFS와 BFS의 가장 궁극적인 차이는 스택에서 선입선출을 할 것인가, 선입후출을 할것인가. 즉, DFS는 스택에서 빼는 과정을 스택의 맨 뒤(선입후출)에서 해주고 BFS는 스택의 맨 앞(선입선출)으로 해준다. 이와 같이 하면 한 정점에서 타고갈수 있는 끝의 정점까지 찍고 가느냐와, 처음 출발 정점부터 시작해 연결된 정점을 모두 탐색해주고 다음 정점으로 넘어가느냐의 차이를 만들어 줄 수 있다`, 는 사실을 깨닳았다.

---

- 루트 노드(혹은 다른 임의의 노드)에서 시작해서 인접한 노드를 먼저 탐색하는 방법
  - 시작 정점으로부터 가까운 정점을 먼저 방문하고 멀리 떨어져 있는 정점을 나중에 방문하는 순회 방법이다.
  - 즉, 깊게(deep) 탐색하기 전에 넓게(wide) 탐색하는 것이다.
  - 사용하는 경우: 두 노드 사이의 최단 경로 혹은 임의의 경로를 찾고 싶을 때 이 방법을 선택한다.
    