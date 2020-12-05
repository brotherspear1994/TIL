# BAEKJOON

# 1157: 단어 공부

### 문제

```python
그래프를 DFS로 탐색한 결과와 BFS로 탐색한 결과를 출력하는 프로그램을 작성하시오. 단, 방문할 수 있는 정점이 여러 개인 경우에는 정점 번호가 작은 것을 먼저 방문하고, 더 이상 방문할 수 있는 점이 없는 경우 종료한다. 정점 번호는 1번부터 N번까지이다.
```



#### 1번 풀이

```python
from _collections import deque
dr = [-1,0,1,0]
dc = [0,-1,0,1]

def dfs(val):
    stack = deque()
    stack.append(val)
    print_cnt = 0
    while stack:
        row = stack.pop()
        if visit_dfs[row] == 0:
            print(row, end=' ')
            print_cnt += 1
            if print_cnt == N: return
        visit_dfs[row] = 1
        remember = 0
        for w in range(len(map[row])):
            if map[row][w] and not visit_dfs[w]:
                stack.append(w)
                remember += 1
        for _ in range(len(stack)):
            k = remember-1
            while k > 0:
                if stack[k] > stack[k-1]:
                    stack[k], stack[k-1] = stack[k-1], stack[k]
                k -= 1
def bfs(val):
    stack = deque()
    stack.append(val)
    print_cnt = 0
    while stack:
        row = stack.popleft()
        if visit_bfs[row] == 0:
            print(row, end=' ')
            print_cnt += 1
            if print_cnt == N: return
        visit_bfs[row] = 1
        remember = 0
        for w in range(len(map[row])):
            if map[row][w] and not visit_bfs[w]:
                stack.append(w)
                remember += 1
        for _ in range(len(stack)):
            k = remember-1
            while k > 0:
                if stack[k] < stack[k-1]:
                    stack[k], stack[k-1] = stack[k-1], stack[k]
                k -= 1

N, M, V = map(int,input().split())
gansun_info = [list(map(int,input().split())) for _ in range(M)]
map = [[0]*(N+1) for _ in range(N+1)]
for r, c in gansun_info:
    map[r][c] = 1
    map[c][r] = 1
# for row in map:
#     print(*row)
visit_dfs = [0]*(N+1)
visit_bfs = [0]*(N+1)
dfs(V)
print()
bfs(V)
print()
```

- 재귀함수를 사용하지 않고 while을 통해 dfs와 bfs를 구현해봤다.

- 백준 문제상에는 런타임 에러가 발생해 2번풀이로 다시 풀어봤다.

  

### 2번 풀이

```python
def dfs(val):
    global dfs_path
    dfs_path += str(val)+' '
    visited[val] = 1
    for i in range(1,N+1):
        if visited[i] == 0 and arr[val][i]:
            dfs(i)
def bfs(val):
    global bfs_path
    q = []
    q.append(val)
    visited[val] = 1
    while q:
        start = q.pop(0)
        bfs_path += str(start) + ' '
        for i in range(1,N+1):
            if visited[i] == 0 and arr[start][i]:
                q.append(i)
                visited[i] = 1

N, M, V = map(int,input().split())
arr = [[0]*(N+1) for _ in range(N+1)]
visited = [0]*(N+1)
for _ in range(M):
    a, b = map(int,input().split())
    arr[a][b] = 1
    arr[b][a] = 1
# for row in arr:
#     print(row)
# print()
dfs_path = ''
bfs_path = ''
dfs(V)
visited = [0]*(N+1)
bfs(V)
print(dfs_path)
print(bfs_path)
```

- 으외로 재귀함수를 이용해 풀었더니 런타임 에러가 발생하지 않고 풀렸다. 상황에 따라 여러방법을 익혀야 하는 중요성을 느꼈다.