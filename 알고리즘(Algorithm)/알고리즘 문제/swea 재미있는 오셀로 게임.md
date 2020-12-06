# swea

# 재미있는 오셀로 게임

### 일자 20200828

### 문제

[본문 링크 참조](https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AWQmA4uK8ygDFAXj&categoryId=AWQmA4uK8ygDFAXj&categoryType=CODE)

#### 풀이

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