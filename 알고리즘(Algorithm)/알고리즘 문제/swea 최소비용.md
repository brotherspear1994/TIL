# swea

# 최소비용

### 일자 20201106

### 문제

출발에서 최종 도착지까지 경유하는 지역의 높이 차이에 따라 연료 소비량이 달라지기 때문에, 최적의 경로로 이동하면 최소한의 연료로 이동할 수 있다.

다음은 각 지역의 높이를 기록한 표의 예로, 항상 출발은 맨 왼쪽 위, 도착지는 가장 오른쪽 아래이며, 각 칸에서는 상하좌우 칸이 나타내는 인접 지역으로만 이동할 수 있다.

(표에 표시되지 않은 지역이나 대각선 방향으로는 이동 불가.)

 

| 0    | 2    | 1    |
| ---- | ---- | ---- |
| 0    | 1    | 1    |
| 1    | 1    | 1    |



인접 지역으로 이동시에는 기본적으로 1만큼의 연료가 들고, 더 높은 곳으로 이동하는 경우 높이 차이만큼 추가로 연료가 소비된다.



| 0    | 2    | 1    |
| ---- | ---- | ---- |
| 0    | 1    | 1    |
| 1    | 1    | 1    |



색이 칠해진 칸을 따라 이동하는 경우 기본적인 연료 소비량 4에, 높이가 0에서 1로 경우만큼 추가 연료가 소비되므로 최소 연료 소비량 5로 목적지에 도착할 수 있다.

이동 가능한 지역의 높이 정보에 따라 최소 연료 소비량을 출력하는 프로그램을 만드시오.


**[입력]**

첫 줄에 테스트 케이스의 개수 T가 주어지고, 테스트 케이스 별로 첫 줄에 표의 가로, 세로 칸수N, 다음 줄부터 N개 지역의 높이 H가 N개의 줄에 걸쳐 제공된다.

1<=T<=50, 3<=N<=100, 0<=H<1000

**[출력]**

각 줄마다 "#T" (T는 테스트 케이스 번호)를 출력한 뒤, 답을 출력한다.

#### 풀이1

```python
dx = [-1,0,1,0]
dy = [0,-1,0,1]

def dfs(x,y,acc):
    global minV
    if acc >= minV:
        return
    if x == N-1 and y == N-1:
        minV = min(acc, minV)
        return
    else:
        for k in range(4):
            nx = x + dx[k]
            ny = y + dy[k]
            if 0 <= nx < N and 0 <= ny < N and not visit[nx][ny]:
                visit[nx][ny] = 1
                if arr[nx][ny] >= arr[x][y]:
                    dfs(nx,ny,acc+1+(arr[nx][ny]-arr[x][y]))
                else:
                    dfs(nx,ny,acc+1)
                visit[nx][ny] = 0

for tc in range(1,int(input())+1):
    N = int(input())
    arr = [list(map(int,input().split())) for _ in range(N)]
    # for row in arr:
    #     print(row)
    # print()
    visit = [[0]*N for _ in range(N)]
    visit[0][0] = 1

    minV = 0xffff
    dfs(0,0,0)
    print("#%d" % tc, minV)
```

- 이 때는 MST Prim과 Dikjkstra를 잘 파악하고 있어서, 해당 유형의 문제가 나오면 공식 대입하듯 뚝딱 풀어냈다.
- 위 풀이는 내가 직접 풀어본 풀이이다.

#### 풀이2

```python
dx = [-1,0,1,0]
dy = [0,-1,0,1]
for tc in range(1,int(input())+1):
    N = int(input())
    arr = [list(map(int,input().split())) for _ in range(N)]

    INF = 0xffff

    key = [[INF]*N for _ in range(N)]
    visit = [[False] * N for _ in range(N)]

    key[0][0] = 0

    while visit[N-1][N-1] == False:
        minV = INF
        minX, minY = -1, -1
        for i in range(N):
            for j in range(N):
                if minV > key[i][j] and not visit[i][j]:
                    minV = key[i][j]
                    minX, minY = i, j
        visit[minX][minY] = True

        for k in range(4):
            nx = minX + dx[k]
            ny = minY + dy[k]

            if 0 <= nx < N and 0 <= ny < N and not visit[nx][ny]:
                if arr[nx][ny] >= arr[minX][minY]:
                    if key[nx][ny] > key[minX][minY] + 1 + (arr[nx][ny] - arr[minX][minY]):
                        key[nx][ny] = key[minX][minY] + 1 + (arr[nx][ny] - arr[minX][minY])
                else:
                    if key[nx][ny] > key[minX][minY]+1:
                        key[nx][ny] = key[minX][minY]+1
    ans = key[N-1][N-1]
    print("#%d" % tc, ans)
```

- 교수님 풀이를 바탕으로 다시 학습해봄.