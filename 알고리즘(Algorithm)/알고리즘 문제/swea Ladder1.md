# swea

# Ladder1

### 일자 20200827

### 문제

[본문 링크 참고하기](https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AV14ABYKADACFAYh&categoryId=AV14ABYKADACFAYh&categoryType=CODE)

#### 풀이1

```python
def search(r,c): #r: row, c: column
    # 왼, 오, 아래
    dr = [0,0,1]
    dc = [-1,1,0]
    num = ladder[r][c]
    visited = [[0 for _ in range(N)] for _ in range(N)]
    visited[r][c] = 1


    while True:
        if num == 2: return True #  찾음을 리턴
        if r == 99: return False # 못찾음을 리턴

        for k in range(3):
            # 새로운 좌표 구하기
            nr = r + dr[k]
            nc = c + dc[k]
            # 범위를 벗어나지 않는가? 사다리인지? 이미 방문했는지?
            if nr < 0 or nr >= N or nc<0 or nc >= N: continue
            if ladder[nr][nc] == 0 :continue
            if visited[nr][nc] == 1: continue
            r = nr
            c = nc
            num = ladder[nr][nc]
            visited[nr][nc] = 1 # 방문표시
            break #갈길을 찾으면 탐색을 종료하고 반복 빠져나감

T = 10
for tc in range(1,T+1):
    N = 100
    int(input()) # tc 제거용
    ladder = [list(map(int,input().split())) for _ in range(N)]
# for row in ladder:
#     print(row)
    cnt = 0
    for i in range(N):
        if ladder[0][i] == 1:
            result = search(0,i)
        if result:
            cnt = i
            break
    print("#{} {}".format(tc, cnt))
```



### 풀이 2

```python
def check(x,y):
    if x < 0 or x>=100 or y <0 or y >=100: return False
    if arr[x][y] == 0: return False
    return True


for tc in range(1,11):
    case_num = input()
    arr = [list(map(int,input().split())) for _ in range(100)]

    # 도착점 찾기
    x = y = 0
    for i in range(100):
        if arr[99][i] == 2:
            x, y = 99, i # 도착첨 저장
            break

    dir = 0 # 방향정보 저장 0: 위, 1: 좌, 2: 우

    while x:
        # 왼쪽에 길이 있는경우
        if dir != 2 and check(x,y-1):
            y -= 1; dir = 1
        # 오른쪽에 길이 있는경우
        elif dir != 1 and check(x,y+1):
            y += 1; dir = 2
        # 그외, 위로 가는 경우
        else:
            x -= 1; dir =0
    print(y)
```

- swea Ladder 1 문제를 풀어본 후 교수님의 풀이까지 학습 후 다시 교수님 풀이로 풀어보았다.
- 두 가지 풀이 방식으로 풀어보았다.
- 방향정보를 자유자재로 다룰수 있게끔 도와주는 유익한 문제였다.



### 재귀 함수 풀이법(추가)

```python
def ladder(x, y):
    if x == 0:
        # global ans; ans= y
        return y
    else:
        while x:
            arr[x][y] = 0
            # 왼쪽으로 가는 경우
            if check(x, y - 1):
                return ladder(x, y - 1)  # ladder2를 적용할경우 +1을이용해서 count 한다
            # 오른쪽으로 가는경우
            elif check(x, y + 1):
                return ladder(x, y + 1)
            # 그외, 위로 가는경우
            else:
                return ladder(x - 1, y)
            # arr[x][y] =1,2 다시 1로 채운다 원상복구시킨다
```

- 재귀 함수를 통해 푸는 방법도 이후에 추가적으로 학습해 git에 남겨본다.