# swea

# 디저트 카페

### 일자 20201107

### 문제

[본문 링크 참조](https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AV5VwAr6APYDFAWu&categoryId=AV5VwAr6APYDFAWu&categoryType=CODE)

#### 풀이1(실패 코드)

```python
dx = [-1,1,1,-1]
dy = [1,1,-1,-1]

def dfs(x,y):
    global boolean_final, ans
    boolean = False
    k = 0

    stack = []
    stack.append(arr[x][y])

    temp_x, temp_y = x, y
    dis_first, dis_second = -1, -1
    dis = 0
    while k <= 3:
        nx, ny = x+dx[k], y+dy[k]
        if nx == temp_x and ny == temp_y:
            boolean = True; break
        if k == 0 or k == 1:
            if 0 <= nx < N and 0 <= ny < N and not arr[nx][ny] in stack:
                stack.append(arr[nx][ny])
                x, y, dis = nx, ny, dis+1
            else:
                if k == 0: dis_first = dis; dis = 0
                elif k == 1: dis_second = dis; dis = 0
                k += 1
                continue
        elif k == 2 or k == 3:
            if k == 2:
                if 0 <= nx < N and 0 <= ny < N and not arr[nx][ny] in stack and dis <= dis_first:
                    stack.append(arr[nx][ny])
                    x, y, dis = nx, ny, dis + 1
                else:
                    k += 1; dis = 0; continue
            elif k == 3:
                if 0 <= nx < N and 0 <= ny < N and not arr[nx][ny] in stack and dis <= dis_second:
                    stack.append(arr[nx][ny])
                    x, y, dis = nx, ny, dis + 1
                else:
                    k += 1; dis = 0; continue
    if boolean:
        if len(stack) >= 4:
            ans = max(ans, len(stack))
            boolean_final = True

for tc in range(1,int(input())+1):
    N = int(input())
    arr = [list(map(int, input().split())) for _ in range(N)]
    ans = -1
    boolean_final = False
    for i in range(N):
        for j in range(N):
            dfs(i,j)
    print(ans)
```

- 이때 당시에 풀었던 방법으로는 모든 테스트케이스들을 통과하지 못해 잠시 보류했다.



#### 풀이2(성공!)

````python
import sys; sys.stdin = open('디저트.txt', 'r')
# 20번이 넘는 디버깅 끝에 3시간만에 문제를 풀었다,,, 다른 사람의 풀이를 참고하지 않고 나만의 힘으로
# 풀어서 뿌듯하긴한데,,,몬가 100퍼센트 왜 이렇게 해야만 답이나오는지는 이해를 하지 못한 느낌이라 주석을 남기며
# 이해해보려고 한다.
dx = [-1,1,1,-1] # 대각선 움직임을 가져가줄 dx, dy
dy = [1,1,-1,-1]


def dfs(x,y,acc):
    global ans
    locs.append((x,y)); foods.append(arr[x][y])
    # 함수로 들어오자마자 해당 좌표는 우선 탐색가능영역에 속했기 때문에 바로 locs와 foods에 넣어준다.
    # 원래는 밑의 if문안에 x,y와 nx, ny 둘다 append하는 것을 시도해봤지만 이럴 경우 최초의 출발점은 체크를 못해주기 때문에
    # 원래는 가서는 안되는 노선 예를 들어 최초가게(9번)과 다음번가게(9번)을 방문해 버리게 된다.
    for k in range(4): # 원래는 for문을 사용하지 않고 direction 정보를 함수의 변수로 사용해 줬지만 이럴 경우에는
        # 적절하지 못한 상황을 만나기 전까지는 한방향으로만 쭈욱 가기 때문에 모든 경우의 수,
        # 예를들어 쭈욱 갈 수 있음에도 불구하고 다른 가능한 방향으로 방향을 트는 경우를 고려해 주지 못하기 떄문에 for문으로 대체했다.
        nx, ny = x+dx[k], y+dy[k] # 갈 방향을 탐색
        if (nx,ny) == start_point and 0 in visit and 1 in visit and 2 in visit:
            # 갈 방향이 처음 좌표와 일치하고, 사각형을 이루기 위한 조건(이전 방향을 한번씩 모두 탄 경우)을 완성한 경우
            acc += 1 # 현재 위치는 아직 counting 되지 않았으므로 현재위치까지 카운팅 해주고
            ans = max(ans, acc) # 최대 값 산출
            return
        if 0<=nx<N and 0<=ny<N and not (nx,ny) in locs and not arr[nx][ny] in foods:
            # 예비방향(탐색좌표)가 범위안에 있고 아직 방문하지 않은 좌표이며, 중복되지 않는 가게일 경우
            if visit: # 적어도 한번은 방향을 튼경우
                if k >= max(visit): # 방향은 최소 한번씩만 탈 수 있으므로(두번이상은 방향을 못틀기 때문에)
                    # 쭈욱직진하거나(지금 방향과 동일하거나) 한번도 안 탄 방향일 경우에만 진행
                    visit.append(k) # 다시 이 방향은 탐색했다는 걸 표시
                    dfs(nx, ny, acc + 1) # nx, ny를 현재좌표로 갱신하고 가게를 세주며, 재귀함수 호출
                    visit.pop(); locs.pop(); foods.pop() # 방금 들어갔던 좌표는 타지 않았다는 가정을 해줘야하므로
                    # pop을 통해 빼내준다.
            elif k == 0: # 최초 방향(오른쪽위 대각선)을 타는 경우
                visit.append(k)
                dfs(nx, ny, acc + 1)
                visit.pop(); locs.pop(); foods.pop()

for tc in range(1,int(input())+1):
    N = int(input()) # 입력
    arr = [list(map(int, input().split())) for _ in range(N)]

    ans = -1 # 경우의 수를 찾을 수 없을때는 -1을 출력
    for i in range(N): # 모든 정점을 출발점으로 dfs탐색을 해본다.
        for j in range(N):
            locs = []; foods = []; visit = [] # 각각 좌표, 음식, 4방탐색을 모두 실시했는지 확인해주는 용
            # 원래는 set을 사용해 줬지만 경우의 수 마다 이전 좌표로는 이동하지 않는다는 가정하에
            # for문을 돌며 pop을 실행시켜줘야 하므로, set은 remove 사용시 계속 오류가 나 리스트로 교체
            start_point = (i,j) # 최초 시작점을 기록(후에 돌아와야 하므로)
            dfs(i,j,0) # 시작좌표와 방문 가게수를 변수로 담아주고 탐색시작.
    print("#{} {}".format(tc, ans))
````

- 20201204 일자에 다시한번 풀었는데 문제를 푸는데 성공했다.
- 시간이 지나며서 꾸준히 실력이 늘었다는 사실을 확인할 수 있었던 시간이었다.!