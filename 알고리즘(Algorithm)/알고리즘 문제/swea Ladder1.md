# swea

# Ladder1

### 일자 20200827

### 문제

점심 시간에 산책을 다니는 사원들은 최근 날씨가 더워져, 사다리 게임을 통하여 누가 아이스크림을 구입할지 결정하기로 한다.

김 대리는 사다리타기에 참여하지 않는 대신 사다리를 그리기로 하였다.

사다리를 다 그리고 보니 김 대리는 어느 사다리를 고르면 X표시에 도착하게 되는지 궁금해졌다. 이를 구해보자.

아래 <그림 1>의 예를 살펴보면, 출발점 x=0 및 x=9인 세로 방향의 두 막대 사이에 임의의 개수의 막대들이 랜덤 간격으로 추가되고(이 예에서는 2개가 추가됨) 이 막대들 사이에 가로 방향의 선들이 또한 랜덤하게 연결된다.

X=0인 출발점에서 출발하는 사례에 대해서 화살표로 표시한 바와 같이, 아래 방향으로 진행하면서 좌우 방향으로 이동 가능한 통로가 나타나면 방향 전환을 하게 된다.

방향 전환 이후엔 다시 아래 방향으로만 이동하게 되며, 바닥에 도착하면 멈추게 된다.

문제의 X표시에 도착하려면 X=4인 출발점에서 출발해야 하므로 답은 4가 된다. 해당 경로는 별도로 표시하였다.


![img](swea 스도쿠 검증.assets/fileDownload.do)

<그림 1> 사다리 게임에 대한 설명 (미니맵)


아래 <그림 2>와 같은 **100 x 100 크기의 2차원 배열로 주어진 사다리에 대해서, 지정된 도착점에 대응되는 출발점 X를 반환하는 코드를 작성하라** (‘0’으로 채워진 평면상에 사다리는 연속된 ‘1’로 표현된다. 도착 지점은 '2'로 표현된다).


 ![img](swea 스도쿠 검증.assets/fileDownload.do)

<그림 2> 테스트 케이스에 의해 생성되는 실제 사다리의 모습


**[제약 사항]**

한 막대에서 출발한 가로선이 다른 막대를 가로질러서 연속하여 이어지는 경우는 없다.

**[입력]**

입력 파일의 첫 번째 줄에는 테스트 케이스의 번호가 주어지며, 바로 다음 줄에 테스트 케이스가 주어진다.

총 10개의 테스트 케이스가 주어진다.

**[출력]**

\#부호와 함께 테스트 케이스의 번호를 출력하고, 공백 문자 후 도착하게 되는 출발점의 x좌표를 출력한다.



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