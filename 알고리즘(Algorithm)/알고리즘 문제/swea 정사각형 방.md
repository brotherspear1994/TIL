# swea

# 정사각형 방

### 일자 20200908

### 문제

N2개의 방이 N×N형태로 늘어서 있다.

위에서 i번째 줄의 왼쪽에서 j번째 방에는 1이상 N2 이하의 수 Ai,j가 적혀 있으며, 이 숫자는 모든 방에 대해 서로 다르다.

당신이 어떤 방에 있다면, 상하좌우에 있는 다른 방으로 이동할 수 있다.

물론 이동하려는 방이 존재해야 하고, 이동하려는 방에 적힌 숫자가 현재 방에 적힌 숫자보다 정확히 1 더 커야 한다.

처음 어떤 수가 적힌 방에서 있어야 가장 많은 개수의 방을 이동할 수 있는지 구하는 프로그램을 작성하라.


**[입력]**

첫 번째 줄에 테스트 케이스의 수 T가 주어진다.

각 테스트 케이스의 첫 번째 줄에는 하나의 정수 N (1 ≤ N ≤ 103)이 주어진다.

다음 N개의 줄에는 i번째 줄에는 N개의 정수 Ai, 1, … , Ai, N (1 ≤ Ai, j ≤ N2) 이 공백 하나로 구분되어 주어진다.

Ai, j는 모두 서로 다른 수이다.


**[출력]**

각 테스트 케이스마다 ‘#x’(x는 테스트케이스 번호를 의미하며 1부터 시작한다)를 출력하고,

한 칸을 띄운 후, 처음에 출발해야 하는 방 번호와 최대 몇 개의 방을 이동할 수 있는지를 공백으로 구분하여 출력한다.

이동할 수 있는 방의 개수가 최대인 방이 여럿이라면 그 중에서 적힌 수가 가장 작은 것을 출력한다.


**[예제 풀이]**

첫 번째 테스트 케이스는 1 또는 3이 적힌 곳에 있어야 한다.

두 번째 테스트 케이스는 3 또는 6이 적힌 곳에 있어야 한다.


#### 풀이1

```python
dr = [-1, 1, 0, 0]
dc = [0, 0, -1, 1]


def move(r, c, cur_move):
    visit = [[0] * (N) for _ in range(N)]
    start_stack = []
    start_stack.append([r, c])
    visit[r][c] = 1
    while start_stack:
        n = start_stack.pop()
        row, col = n[0], n[1]
        for k in range(4):
            nr = row + dr[k]
            nc = col + dc[k]
            if nr >= 0 and nr < N and nc >= 0 and nc < N:
                if visit[nr][nc] == 0 and rooms[nr][nc] == rooms[row][col] + 1:
                    start_stack.append([nr, nc])
                    visit[nr][nc] = 1
                    cur_move += 1
    return cur_move


T = int(input())
for tc in range(1, T + 1):
    N = int(input())
    rooms = [list(map(int, input().split())) for _ in range(N)]
    # for row in rooms:
    #     print(row)
    # print()
    max_move = 0
    max_idx = [0, 0]
    for i in range(N):
        for j in range(N):
            max_sub = move(i, j, 1)
            if max_move < max_sub:
                max_move = max_sub
                max_idx = [i, j]
            elif max_move == max_sub:
                if rooms[max_idx[0]][max_idx[1]] > rooms[i][j]:
                    max_idx = [i, j]
                else:
                    continue
    room_number = rooms[max_idx[0]][max_idx[1]]
    print("#{} {} {}".format(tc, room_number, max_move))
```



#### 풀이2(20201107)

```python
from collections import deque

dx = [-1,0,1,0]
dy = [0,-1,0,1]

def bfs(x, y):
    cnt = 0
    Q = deque()
    Q.append((x,y))
    while Q:
        x,y = Q.popleft()
        for k in range(4):
            nx = x+dx[k]
            ny = y+dy[k]
            if 0<= nx < N and 0<= ny < N and arr[nx][ny] == arr[x][y]+1:
                Q.append((nx,ny)); cnt+=1
    return cnt


for tc in range(1,int(input())+1):
    N = int(input())
    arr = [list(map(int, input().split())) for _ in range(N)]
    # for row in arr:
    #     print(row)
    # print()
    max_cnt = 0
    min_room_num = 0xfffffff
    ans_x = -1
    ans_y = -1
    for i in range(N):
        for j in range(N):
            cnt = bfs(i,j)
            if cnt > max_cnt:
                min_room_num = arr[i][j]
                max_cnt = cnt
                ans_x = i
                ans_y = j
            elif cnt == max_cnt:
                if arr[i][j] < min_room_num:
                    min_room_num = arr[i][j]
                    ans_x = i
                    ans_y = j

    print("#{} {} {}".format(tc, arr[ans_x][ans_y], max_cnt+1))
```