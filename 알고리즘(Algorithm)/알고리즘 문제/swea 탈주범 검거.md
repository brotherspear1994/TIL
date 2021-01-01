# swea

# 탈주범 검거

### 일자 20201106

### 문제

[원본 링크 참조](https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AV5PpLlKAQ4DFAUq&categoryId=AV5PpLlKAQ4DFAUq&categoryType=CODE)

#### 풀이1

```python
from collections import deque

for tc in range(1,int(input())+1):
    N, M, R, C, L = map(int,input().split())
    tunnels = [list(map(int,input().split())) for _ in range(N)]
    # for row in tunnels:
    #     print(row)
    # print()
    visit = [[0]*M for _ in range(N)]
    visit[R][C] = 1
    bfs(R, C, 0)
    ans = 0
    for row in visit:
        ans += sum(row)
    print("#{} {}".format(tc, ans))


def dfs(x, y, time):
    if time == L-1:
        return
    else:
        if tunnels[x][y] == 1:
            dx = [-1,0,1,0]
            dy = [0,-1,0,1]
            for k in range(4):
                nx = x+dx[k]
                ny = y+dy[k]
                if 0<= nx < N and 0 <= ny < M:
                    if k == 0:
                        if tunnels[nx][ny] == 1 or tunnels[nx][ny] == 2 or tunnels[nx][ny] == 5 or tunnels[nx][ny] == 6:
                            visit[nx][ny] = 1
                            dfs(nx,ny,time+1)
                    if k == 1:
                        if tunnels[nx][ny] == 1 or tunnels[nx][ny] == 3 or tunnels[nx][ny] == 4 or tunnels[nx][ny] == 5:
                            visit[nx][ny] = 1
                            dfs(nx,ny,time+1)
                    if k == 2:
                        if tunnels[nx][ny] == 1 or tunnels[nx][ny] == 2 or tunnels[nx][ny] == 4 or tunnels[nx][ny] == 7:
                            visit[nx][ny] = 1
                            dfs(nx,ny,time+1)
                    if k == 3:
                        if tunnels[nx][ny] == 1 or tunnels[nx][ny] == 3 or tunnels[nx][ny] == 6 or tunnels[nx][ny] == 7:
                            visit[nx][ny] = 1
                            dfs(nx,ny,time+1)
        elif tunnels[x][y] == 2:
            dx = [-1,1]
            dy = [0,0]
            for k in range(2):
                nx = x+dx[k]
                ny = y+dy[k]
                if 0 <= nx < N and 0 <= ny < M:
                    if k == 0:
                        if tunnels[nx][ny] == 1 or tunnels[nx][ny] == 2 or tunnels[nx][ny] == 5 or tunnels[nx][ny] == 6:
                            visit[nx][ny] = 1
                            dfs(nx,ny,time+1)
                    if k == 1:
                        if tunnels[nx][ny] == 1 or tunnels[nx][ny] == 2 or tunnels[nx][ny] == 4 or tunnels[nx][ny] == 7:
                            visit[nx][ny] = 1
                            dfs(nx,ny,time+1)
        elif tunnels[x][y] == 3:
            dx = [0,0]
            dy = [-1,1]
            for k in range(2):
                nx = x + dx[k]
                ny = y + dy[k]
                if 0 <= nx < N and 0 <= ny < M:
                    if k == 0:
                        if tunnels[nx][ny] == 1 or tunnels[nx][ny] == 3 or tunnels[nx][ny] == 4 or tunnels[nx][ny] == 5:
                            visit[nx][ny] = 1
                            dfs(nx, ny, time + 1)
                    if k == 1:
                        if tunnels[nx][ny] == 1 or tunnels[nx][ny] == 3 or tunnels[nx][ny] == 6 or tunnels[nx][ny] == 7:
                            visit[nx][ny] = 1
                            dfs(nx, ny, time + 1)
        elif tunnels[x][y] == 4:
            dx = [-1,0]
            dy = [0,1]
            for k in range(2):
                nx = x + dx[k]
                ny = y + dy[k]
                if 0 <= nx < N and 0 <= ny < M:
                    if k == 0:
                        if tunnels[nx][ny] == 1 or tunnels[nx][ny] == 2 or tunnels[nx][ny] == 5 or tunnels[nx][ny] == 6:
                            visit[nx][ny] = 1
                            dfs(nx, ny, time + 1)
                    if k == 1:
                        if tunnels[nx][ny] == 1 or tunnels[nx][ny] == 3 or tunnels[nx][ny] == 6 or tunnels[nx][ny] == 7:
                            visit[nx][ny] = 1
                            dfs(nx, ny, time + 1)
        elif tunnels[x][y] == 5:
            dx = [1,0]
            dy = [0,1]
            for k in range(2):
                nx = x + dx[k]
                ny = y + dy[k]
                if 0 <= nx < N and 0 <= ny < M:
                    if k == 0:
                        if tunnels[nx][ny] == 1 or tunnels[nx][ny] == 2 or tunnels[nx][ny] == 4 or tunnels[nx][ny] == 7:
                            visit[nx][ny] = 1
                            dfs(nx, ny, time + 1)
                    if k == 1:
                        if tunnels[nx][ny] == 1 or tunnels[nx][ny] == 3 or tunnels[nx][ny] == 6 or tunnels[nx][ny] == 7:
                            visit[nx][ny] = 1
                            dfs(nx, ny, time + 1)
        elif tunnels[x][y] == 6:
            dx = [1,0]
            dy = [0,-1]
            for k in range(2):
                nx = x + dx[k]
                ny = y + dy[k]
                if 0 <= nx < N and 0 <= ny < M:
                    if k == 0:
                        if tunnels[nx][ny] == 1 or tunnels[nx][ny] == 2 or tunnels[nx][ny] == 4 or tunnels[nx][ny] == 7:
                            visit[nx][ny] = 1
                            dfs(nx, ny, time + 1)
                    if k == 1:
                        if tunnels[nx][ny] == 1 or tunnels[nx][ny] == 3 or tunnels[nx][ny] == 4 or tunnels[nx][ny] == 5:
                            visit[nx][ny] = 1
                            dfs(nx, ny, time + 1)
        elif tunnels[x][y] == 7:
            dx = [-1,0]
            dy = [0,-1]
            for k in range(2):
                nx = x + dx[k]
                ny = y + dy[k]
                if 0 <= nx < N and 0 <= ny < M:
                    if k == 0:
                        if tunnels[nx][ny] == 1 or tunnels[nx][ny] == 2 or tunnels[nx][ny] == 5 or tunnels[nx][ny] == 6:
                            visit[nx][ny] = 1
                            dfs(nx, ny, time + 1)
                    if k == 1:
                        if tunnels[nx][ny] == 1 or tunnels[nx][ny] == 3 or tunnels[nx][ny] == 4 or tunnels[nx][ny] == 5:
                            visit[nx][ny] = 1
                            dfs(nx, ny, time + 1)
for tc in range(1,int(input())+1):
    N, M, R, C, L = map(int,input().split())
    tunnels = [list(map(int,input().split())) for _ in range(N)]
    # for row in tunnels:
    #     print(row)
    # print()
    visit = [[0]*M for _ in range(N)]
    visit[R][C] = 1
    dfs(R, C, 0)
    ans = 0
    for row in visit:
        ans += sum(row)
    print("#{} {}".format(tc, ans))
```

- 이 때는 MST Prim과 Dikjkstra를 잘 파악하고 있어서, 해당 유형의 문제가 나오면 공식 대입하듯 뚝딱 풀어냈다.
- 위 풀이는 내가 직접 풀어본 풀이이다. DFS 방식으로 풀었다.
- 문제의 설명을 잘 읽고 각 케이스별로 조건문을 잘 나눠줬다.

#### 풀이2

```python
def bfs(x, y, time):
    Q = deque()
    Q.append((x,y,time))
    while Q:
        x, y, time = Q.popleft()
        if time == L-1:
            continue
        else:
            if tunnels[x][y] == 1:
                dx = [-1,0,1,0]
                dy = [0,-1,0,1]
                for k in range(4):
                    nx = x+dx[k]
                    ny = y+dy[k]
                    if 0<= nx < N and 0 <= ny < M and not visit[nx][ny]:
                        if k == 0:
                            if tunnels[nx][ny] == 1 or tunnels[nx][ny] == 2 or tunnels[nx][ny] == 5 or tunnels[nx][ny] == 6:
                                visit[nx][ny] = 1
                                Q.append((nx,ny,time+1))
                        if k == 1:
                            if tunnels[nx][ny] == 1 or tunnels[nx][ny] == 3 or tunnels[nx][ny] == 4 or tunnels[nx][ny] == 5:
                                visit[nx][ny] = 1
                                Q.append((nx,ny,time+1))
                        if k == 2:
                            if tunnels[nx][ny] == 1 or tunnels[nx][ny] == 2 or tunnels[nx][ny] == 4 or tunnels[nx][ny] == 7:
                                visit[nx][ny] = 1
                                Q.append((nx,ny,time+1))
                        if k == 3:
                            if tunnels[nx][ny] == 1 or tunnels[nx][ny] == 3 or tunnels[nx][ny] == 6 or tunnels[nx][ny] == 7:
                                visit[nx][ny] = 1
                                Q.append((nx,ny,time+1))
            elif tunnels[x][y] == 2:
                dx = [-1,1]
                dy = [0,0]
                for k in range(2):
                    nx = x+dx[k]
                    ny = y+dy[k]
                    if 0 <= nx < N and 0 <= ny < M and not visit[nx][ny]:
                        if k == 0:
                            if tunnels[nx][ny] == 1 or tunnels[nx][ny] == 2 or tunnels[nx][ny] == 5 or tunnels[nx][ny] == 6:
                                visit[nx][ny] = 1
                                Q.append((nx,ny,time+1))
                        if k == 1:
                            if tunnels[nx][ny] == 1 or tunnels[nx][ny] == 2 or tunnels[nx][ny] == 4 or tunnels[nx][ny] == 7:
                                visit[nx][ny] = 1
                                Q.append((nx,ny,time+1))
            elif tunnels[x][y] == 3:
                dx = [0,0]
                dy = [-1,1]
                for k in range(2):
                    nx = x + dx[k]
                    ny = y + dy[k]
                    if 0 <= nx < N and 0 <= ny < M and not visit[nx][ny]:
                        if k == 0:
                            if tunnels[nx][ny] == 1 or tunnels[nx][ny] == 3 or tunnels[nx][ny] == 4 or tunnels[nx][ny] == 5:
                                visit[nx][ny] = 1
                                Q.append((nx,ny,time+1))
                        if k == 1:
                            if tunnels[nx][ny] == 1 or tunnels[nx][ny] == 3 or tunnels[nx][ny] == 6 or tunnels[nx][ny] == 7:
                                visit[nx][ny] = 1
                                Q.append((nx,ny,time+1))
            elif tunnels[x][y] == 4:
                dx = [-1,0]
                dy = [0,1]
                for k in range(2):
                    nx = x + dx[k]
                    ny = y + dy[k]
                    if 0 <= nx < N and 0 <= ny < M and not visit[nx][ny]:
                        if k == 0:
                            if tunnels[nx][ny] == 1 or tunnels[nx][ny] == 2 or tunnels[nx][ny] == 5 or tunnels[nx][ny] == 6:
                                visit[nx][ny] = 1
                                Q.append((nx,ny,time+1))
                        if k == 1:
                            if tunnels[nx][ny] == 1 or tunnels[nx][ny] == 3 or tunnels[nx][ny] == 6 or tunnels[nx][ny] == 7:
                                visit[nx][ny] = 1
                                Q.append((nx,ny,time+1))
            elif tunnels[x][y] == 5:
                dx = [1,0]
                dy = [0,1]
                for k in range(2):
                    nx = x + dx[k]
                    ny = y + dy[k]
                    if 0 <= nx < N and 0 <= ny < M and not visit[nx][ny]:
                        if k == 0:
                            if tunnels[nx][ny] == 1 or tunnels[nx][ny] == 2 or tunnels[nx][ny] == 4 or tunnels[nx][ny] == 7:
                                visit[nx][ny] = 1
                                Q.append((nx,ny,time+1))
                        if k == 1:
                            if tunnels[nx][ny] == 1 or tunnels[nx][ny] == 3 or tunnels[nx][ny] == 6 or tunnels[nx][ny] == 7:
                                visit[nx][ny] = 1
                                Q.append((nx,ny,time+1))
            elif tunnels[x][y] == 6:
                dx = [1,0]
                dy = [0,-1]
                for k in range(2):
                    nx = x + dx[k]
                    ny = y + dy[k]
                    if 0 <= nx < N and 0 <= ny < M and not visit[nx][ny]:
                        if k == 0:
                            if tunnels[nx][ny] == 1 or tunnels[nx][ny] == 2 or tunnels[nx][ny] == 4 or tunnels[nx][ny] == 7:
                                visit[nx][ny] = 1
                                Q.append((nx,ny,time+1))
                        if k == 1:
                            if tunnels[nx][ny] == 1 or tunnels[nx][ny] == 3 or tunnels[nx][ny] == 4 or tunnels[nx][ny] == 5:
                                visit[nx][ny] = 1
                                Q.append((nx,ny,time+1))
            elif tunnels[x][y] == 7:
                dx = [-1,0]
                dy = [0,-1]
                for k in range(2):
                    nx = x + dx[k]
                    ny = y + dy[k]
                    if 0 <= nx < N and 0 <= ny < M and not visit[nx][ny]:
                        if k == 0:
                            if tunnels[nx][ny] == 1 or tunnels[nx][ny] == 2 or tunnels[nx][ny] == 5 or tunnels[nx][ny] == 6:
                                visit[nx][ny] = 1
                                Q.append((nx,ny,time+1))
                        if k == 1:
                            if tunnels[nx][ny] == 1 or tunnels[nx][ny] == 3 or tunnels[nx][ny] == 4 or tunnels[nx][ny] == 5:
                                visit[nx][ny] = 1
                                Q.append((nx,ny,time+1))

for tc in range(1,int(input())+1):
    N, M, R, C, L = map(int,input().split())
    tunnels = [list(map(int,input().split())) for _ in range(N)]
    # for row in tunnels:
    #     print(row)
    # print()
    visit = [[0]*M for _ in range(N)]
    visit[R][C] = 1
    bfs(R, C, 0)
    ans = 0
    for row in visit:
        ans += sum(row)
    print("#{} {}".format(tc, ans))
```

- 교수님 풀이를 바탕으로 한번 더 풀어보았다.
- 위는 BFS 방식으로 푼 방법이다.