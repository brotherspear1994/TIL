# swea

# 미로의 거리

### 일자 20200903

### 문제

NxN 크기의 미로에서 출발지 목적지가 주어진다.

이때 최소 몇 개의 칸을 지나면 출발지에서 도착지에 다다를 수 있는지 알아내는 프로그램을 작성하시오.

경로가 있는 경우 출발에서 도착까지 가는데 지나야 하는 최소한의 칸 수를, 경로가 없는 경우 0을 출력한다.

다음은 5x5 미로의 예이다. 1은 벽, 0은 통로를 나타내며 미로 밖으로 벗어나서는 안된다.

13101
10101
10101
10101
10021

마지막 줄의 2에서 출발해서 0인 통로를 따라 이동하면 맨 윗줄의 3에 5개의 칸을 지나 도착할 수 있다.


**[입력]**

첫 줄에 테스트 케이스 개수 T가 주어진다. 1<=T<=50

다음 줄부터 테스트 케이스의 별로 미로의 크기 N과 N개의 줄에 걸쳐 미로의 통로와 벽에 대한 정보가 주어진다. 5<=N<=100

0은 통로, 1은 벽, 2는 출발, 3은 도착이다.

**[출력]**

각 줄마다 "#T" (T는 테스트 케이스 번호)를 출력한 뒤, 답을 출력한다.



### 풀이1

```python
'''
3
5
13101
10101
10101
10101
10021
5
10031
10111
10101
10101
12001
5
00013
01110
21000
01111
00000
'''
dr = [-1,0,1,0]
dc = [0,-1,0,1]

def search(r,c):
    Q = []
    Q.append([r,c])
    distance[r][c] = 0
    visited[r][c] = 5
    while Q:
        start = Q.pop(0)
        new_r, new_c = start[0], start[1]
        for k in range(4):
            nr = new_r + dr[k]
            nc = new_c + dc[k]
            if nr >= 0 and nr < N and nc >= 0 and nc < N:
                if maze[nr][nc] == 0 and visited[nr][nc] != 5:
                    Q.append([nr,nc])
                    distance[nr][nc] = distance[new_r][new_c]+1
                    visited[nr][nc] = 5
                if maze[nr][nc] == 3:
                    return distance[new_r][new_c]
    return 0


T = int(input())
for tc in range(1,T+1):
    N = int(input())
    maze = [list(map(int,input())) for _ in range(N)]
    # for row in maze:
    #     print(row)
    # print()
    distance = [[0]*N for _ in range(N)]
    visited = [[0]*N for _ in range(N)]
    ans = 0
    for i in range(N):
        for j in range(N):
            if maze[i][j] == 2:
                ans = search(i, j)
    # for row in visited:
    #     print(row)
    # print()
    # for row in distance:
    #     print(row)
    # print()
    print("#{} {}".format(tc, ans))
```



### 풀이2

```python
def dfs(sr,sc):
    # 사방 탐색을 위한델타
    dr = [-1,0,1,0]
    dc = [0,1,0,-1]
    s = []
    s.append([sr,sc])
    while len(s) != 0:
        n = s.pop()
        for k in range(4):
            nr = n[0] + dr[k]
            nc = n[1] + dc[k]
            if nr >= 0 and nr < N and nc >=0 and nc<N:
                if arr[nr][nc] == 3:
                    return 1
                elif arr[nr][nc] == 0:
                    s.append([nr,nc])
                    arr[nr][nc] = 1
    return 'error'


T = int(input())
for tc in range(1,T+1):
    N = int(input())
    arr = [[int(x) for x in input()] for _ in range(N)]
    # for row in arr:
    #     print(row)
    sr,sc = 0,0
    for i in range(N):
        for j in range(N):
            if arr[i][j] == 2: #탐색시작
                sr,sc=i,j
    ans = dfs(sr,sc)
    print("#{} {}".format(tc, ans))
```

- DFS 혹은 BFS 스택을 이용해 미로의 거리를 구하는 매우 기본적인 DFS, BFS 문제이다.
- 미로를 이동할 때는 델타 무브를 이용해 사방탐색을 실시해 주면 된다.
- 난이도가 낮고 매우 기본적인 문제라고 할 수있다.



#### 풀이3

```python
dr = [-1,0,1,0]
dc = [0,-1,0,1]
def bfs(row,col,dis):
    global ans_bool
    global final_dis

    maze[row][col] = 1
    dis += 1
    for k in range(4):
        nr = row + dr[k]
        nc = col + dc[k]
        if 0 <= nr < N and 0 <= nc < N and maze[nr][nc] == 0:
            bfs(nr, nc, dis)
        elif 0 <= nr < N and 0 <= nc < N and maze[nr][nc] == 3:
            ans_bool = True
            final_dis = dis

for tc in range(1, int(input())+1):
    N = int(input())
    maze = [list(map(int, input())) for _ in range(N)]
    # for m in maze:
    #     print(m)
    # print()
    final_dis = 0
    ans_bool = False
    for i in range(N):
        for j in range(N):
            if maze[i][j] == 2:
                ans = bfs(i,j,-1)
    if ans_bool:
        print('#{} {}'.format(tc, final_dis))
    else:
        print('#{} 0'.format(tc))
```

- 추가 학습 내용