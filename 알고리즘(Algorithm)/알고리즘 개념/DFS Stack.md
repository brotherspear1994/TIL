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

