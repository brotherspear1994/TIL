# DFS_stack

[TOC]

### DFS_stack 코드

```python
'''
7 8
1 2 1 3 2 4 2 5 4 6 5 6 6 7 3 7
'''

def dfs(n,V):
    stack = [0] * V
    visited = [0] * (V+1)
    top = -1

    top += 1
    stack[top] = n
    while top >= 0:
        n = stack[top]
        top -= 1
        print(n, end=' ')
        for w in range(1,V+1):
            if adj[n][w] != 0 and visited[w] == 0:
                top += 1
                stack[top] = w
                visited[w] = 1


V,E = map(int,input().split())
# 인접행렬 생성
adj = [[0] * (V+1) for _ in range(V+1)]

edges = list(map(int, input().split()))
for i in range(E):
    n1, n2 = edges[i*2], edges[i*2+1]
    adj[n1][n2] = 1
    adj[n2][n1] = 1

dfs(1,V) # 1번 정점을 시작으로 순회할래
```

- 재귀함수가 아닌 while문과 stack을 활용한 깊이우선 탐색에 대한 개념학습과 코드를 직접 짜보았다.
- 학습 후 에는 나 혼자 코드를 짜보는 시간도 가져보았다.



### while문과 재귀함수(For 문)을 이용한 DFS STACK 인접행렬 추가학습

```python
'''
7 8
1 2 1 3 2 4 2 5 4 6 5 6 6 7 3 7
'''

def dfs(val):
    visit[val] = 1
    print(val, end=' ')
    for i in range(N+1):
        if arr[val][i] and not visit[i]:
            stack_dfs.append(i)
    if stack_dfs:
        new_val = stack_dfs.pop()
        dfs(new_val)

N, E = map(int, input().split())
info = list(map(int,input().split()))

arr = [[0]*(N+1) for _ in range(N+1)]

for i in range(E):
    row, col = info[2*i], info[2*i+1]
    arr[row][col] = 1

visit = [0]*(N+1)
stack_dfs = []
# dfs(1)
stack = [1]
while stack:
    start = stack.pop()
    visit[start] = 1
    print(start, end=' ')
    for j in range(N+1):
        if arr[start][j] and visit[j] == 0:
            stack.append(j)
```

#### **깊이 우선 탐색 (DFS, Depth-First Search)**

#### **:** **최대한 깊이 내려간 뒤, 더이상 깊이 갈 곳이 없을 경우 옆으로 이동**

![img](DFS Stack.assets/img.gif)

**💡 깊이 우선 탐색의 개념**

루트 노드(혹은 다른 임의의 노드)에서 시작해서 다음 분기(branch)로 넘어가기 전에

**해당 분기를 완벽하게 탐색**하는 방식을 말합니다.

 

예를 들어, 미로찾기를 할 때 최대한 한 방향으로 갈 수 있을 때까지 쭉 가다가

더 이상 갈 수 없게 되면 다시 가장 가까운 갈림길로 돌아와서

그 갈림길부터 다시 다른 방향으로 탐색을 진행하는 것이 깊이 우선 탐색 방식이라고 할 수 있습니다.

 

1. 모든 노드를 방문하고자 하는 경우에 이 방법을 선택함

2. 깊이 우선 탐색(DFS)이 너비 우선 탐색(BFS)보다 **좀 더 간단함**

3. 검색 속도 자체는 너비 우선 탐색(BFS)에 비해서 **느림**