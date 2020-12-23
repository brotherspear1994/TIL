# swea

# 최소합

### 일자 20201103

#### 문제

그림처럼 NxN 칸에 숫자가 적힌 판이 주어지고, 각 칸에서는 오른쪽이나 아래로만 이동할 수 있다.

맨 왼쪽 위에서 오른쪽 아래까지 이동할 때, 지나는 칸에 써진 숫자의 합계가 최소가 되도록 움직였다면 이때의 합계가 얼마인지 출력하는 프로그램을 만드시오.
 

| 1    | 2    | 3    |
| ---- | ---- | ---- |
| 2    | 3    | 4    |
| 3    | 4    | 5    |


그림의 경우 1, 2, 3, 4, 5순으로 움직이고 최소합계는 15가 된다. 가능한 모든 경로에 대해 합을 계산한 다음 최소값을 찾아도 된다.

**[입력]**

첫 줄에 테스트케이스의 수 T가 주어진다. 1<=T<=50

다음 줄부터 테스트 케이스의 별로 첫 줄에 가로 세로 칸 수 N이 주어지고, 다음 줄부터 N개씩 N개의 줄에 걸쳐 10이하의 자연수가 주어진다. 3<=N<=13
 
**[출력]**

각 줄마다 "#T" (T는 테스트 케이스 번호)를 출력한 뒤, 답을 출력한다.



#### 풀이1

```python
from collections import deque

for tc in range(1,int(input())+1):
    N = int(input())
    square = [list(map(int, input().split())) for _ in range(N)]
    Q = deque()
    Q.append([0,0, square[0][0]])
    min_num = 0xfffff
    while Q:
        x,y,acc = Q.popleft()
        if acc > min_num: continue
        if x == N-1 and y == N-1:
            min_num = min(min_num, acc)
        else:
            if x+1 < N:
                Q.append([x+1,y,acc+square[x+1][y]])
            if y+1 < N:
                Q.append([x,y+1,acc+square[x][y+1]])
    print("#{} {}".format(tc,min_num))
```



#### 풀이2

```python
def move(row, col, acc):
    global min_sum
    if acc > min_sum:
        return
    if row == N-1 and col == N-1:
        if acc < min_sum: min_sum = acc
        return
    nr = row + 1
    nc = col + 1
    if 0<= nr < N:
        move(nr, col, acc+square[nr][col])
    if 0<= nc < N:
        move(row, nc, acc+square[row][nc])

for tc in range(1,int(input())+1):
    N = int(input())
    square = [list(map(int, input().split())) for _ in range(N)]
    # for s in square:
    #     print(s)
    # print()
    min_sum = 0xffffff
    move(0, 0, square[0][0])
    print("#{} {}".format(tc, min_sum))
```



#### 풀이3(교수님 풀이)

```python
for tc in range(1,int(input())+1):
    N = int(input())
    square = [list(map(int, input().split())) for _ in range(N)]

    ans = 0xfffffff
    def minSum(x,y):
        if x == 0 and y == 0:
            return square[0][0]
        if square[x][y] != -1: return square[x][y]
        up=left=0xfffff
        if x-1 >= 0:
            up = minSum(x-1,y)
        if y-1 >=0:
            left = minSum(x,y-1)
        square[x][y] = min(up, left) + square[x][y]
        return square[x][y]
    ans = minSum(N-1, N-1)
    print(ans)
```

- 나 같은 경우는, `1. BFS탐색을 활용해 큐를 생성한뒤 while문을 써 풀기 2. 재귀함수를 이용해 풀기. ` 다음과 같이 두 가지 방식으로 문제를 풀어봤다.
- 이후 교수님의 풀이 수업도 들은 후, 교수님 풀이를 혼자 연습해보며 체화시키는 시간도 가졌다.