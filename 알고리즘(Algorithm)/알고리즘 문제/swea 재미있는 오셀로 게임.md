# swea

# 재미있는 오셀로 게임

### 일자 20200828

### 문제

[본문 링크 참조](https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AWQmA4uK8ygDFAXj&categoryId=AWQmA4uK8ygDFAXj&categoryType=CODE)

#### 풀이1

```python
delta = ((0,1),(1,0),(-1,0),(0,-1),(1,1),(-1,1),(-1,-1),(1,-1))
T = int(input())
for tc in range(1,T+1):
    n, m = map(int,input().split())
    board = [[0] * n for _ in range(n)]

    # mid는 현재 보드 크기의 절반
    mid = n//2
    # 맨처음 초기 흰색돌 두개와 검은색 돌 두개를 엇갈라 놓는다.
    board[mid][mid] = 2
    board[mid-1][mid-1] = 2
    board[mid-1][mid] = 1
    board[mid][mid-1] = 1
    # for row in board:
    #     print(row)

    for i in range(m): #m만큼 돌을 놓는데
        x,y,c = map(int,input().split()) # 보드에 놓을 행,열,색을 입력받는다.
        x,y = x-1,y-1 # 문제에서는 좌표 표기를 1부터 시작하나, board는 0부터 시작하므로 3,2이이면 실제 2,1에 둬야함.

        reverse = [] #뒤집어야 할 돌을 저장할 스택

        for i in range(8):
            dx, dy = delta[i]
            nx, ny = x + dx, y + dy
            while True:
                if nx < 0 or ny < 0 or nx > n-1 or ny > n-1: # 바둑판의 범위를 벗어나면
                    reverse = []
                    break
                if board[nx][ny] == 0: # 빈 칸을 만나는경우 reverse를 초기화
                    reverse = []
                    break
                if board[nx][ny] == c: break # 같은색은 못바꾸니간 break
                else: reverse.append((nx,ny))
                print(reverse)
                print(nx, ny)
                nx, ny  = nx + dx, ny + dy
            for rx, ry in reverse: # 색깔 뒤집기
                if c == 1:
                    board[rx][ry] = 1
                else: board[rx][ry] = 2
            for row in board:
                print(row)
            print(nx,ny)
            print()
        board[x][y] = c
    # 각각의 돌 숫자 세기
    # for row in board:
    #     print(row)
    w, b = 0, 0
    for i in range(n):
        for j in range(n):
            if board[i][j] == 1:
                w += 1
            elif board[i][j] == 2:
                b += 1
    print("#{} {} {}".format(tc, w, b))
```

- 당시 기억으로는 꽤 어려웠던 문제로 기억한다.
- 평소와는 다르게 설명은 주석을 통해 달아놓았다.(시험이나 중요한 문제를 제외한 평소 연습문제를 풀때는 문제를 많이 풀어보는게 중요하다 생각해 시간을 할애해 주석을 잘 달지는 않는다.)

### 풀이2

```python
dr = [-1,-1,0,1,1,1,0,-1]
dc = [0,1,1,1,0,-1,-1,-1]

def check(i,j,color):
    for k in range(8): # 델타 길이 만큼 반복
        ni, nj = i + dr[k], j + dc[k] # 탐색할 좌표 계산
        changeList = [] # 변경할 좌표 리스트
        needtochange = False # 변경여부를 저장

        # 한 방향으로 결정되면 꼭 나아가면서 돌을 변경할 준비
        while ni >= 0 and ni < N and nj >= 0 and nj < N: # 보드안에서 반복
            if board[ni][nj] == 0:
                break
            if board[ni][nj] == color: # 새로놓은 돌과 탐색한 돌색이 같으면
                needtochange = True    # 변경을 해야한다고 표시
                break
            else:
                changeList.append([ni,nj])
                ni = ni+dr[k]
                nj = nj+dc[k]

        if needtochange and changeList:
            for c in changeList:
                board[c[0]][c[1]] = color

T = int(input())
for tc in range (1,T+1):
    N, M = map(int,input().split())
    board = [[0 for _ in range(N)] for _ in range(N)]
    center = N // 2
    board[center-1][center-1] = 2
    board[center][center] = 2
    board[center-1][center] = 1
    board[center][center-1] = 1

    # for row in board:
    #     print(row)

    for k in range(M):
        j,i,color = map(int,input().split())
        board[i-1][j-1] = color
        # for row in board:
        #     print(row)
        check(i-1,j-1,color)
    # 게임종료 후 돌갯수 세기
    cnt_b = 0
    cnt_w = 0
    for i in range(len(board)):
        for j in range(len(board)):
            if board[i][j] == 1: cnt_b += 1
            if board[i][j] == 2: cnt_w += 2
    print("#{} {} {}".format(tc, cnt_b, cnt_w))
```

- 처음 문제를 풀고 난 후, 교수님의 풀이방식도 익혀봤다.
- 첫번째 방식과 매우 유사해 보이지만, 이번에는 check함수를 별도로 만들어 그 안에서 게임을 실행시키고, 게임 종료 후에는 돌의 갯수만 세어주면 되는 방식이다.
- 구성상 교수님의 풀이가 조금 더 깔끔한 느낌이 나, 개인 시간 동안 교수님의 풀이법도 혼자 학습해 봤다.