# swea

# 벽돌 깨기

### 일자 20201203

### 문제

[본문 링크 참조](https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AWXRQm6qfL0DFAUo&categoryId=AWXRQm6qfL0DFAUo&categoryType=CODE)

#### 풀이

```python
import sys; sys.stdin = open('벽돌.txt', 'r')

# 시뮬레이션 문제, 4시간이 걸려 풀었다... 다른이의 풀이를 참고하지 않고 나혼자만의 힘으로 풀어서 뿌듯하긴 하다!

import copy; from collections import deque

def bfs(arr, cnt):
    global ans
    final_bool = 0 # 모든 벽돌이 N번의 횟수를 채우기 전에 파괴될 경우를 대비해 final_bool 설정
    for row in arr:
        final_bool += sum(row)
    if cnt == N or final_bool == 0: # 발포횟수만큼 쐈거나, 모든벽돌이 이미 부서진 경우,
        ans_sub = 0
        for row in arr:
            for j in range(len(row)):
                if row[j]: ans_sub += 1
        ans = min(ans, ans_sub) # 남아있는 벽돌을 세준 뒤 ans값으로 최신화 시켜준다.
        return
    for j in range(W): # 모든 열에 대해서 쏴보는 경우(모든 경우의 수)를 파악할 것이므로 너비만큼 쏜다는 한번씩 쏜다는 가정하에
        temp = copy.deepcopy(arr) # 폭탄이 터지고 내려앉으면서 정보가 갱신되는데, 각 경우마다 정보를 갱신시켜줄 temp 배열을 deepcopy를 이용해 만들어준다.
        s_row = -1 # 폭탄을 쏘고 밑으로 쭉 내려가야한다.
        meet = False # 첫번째 벽돌을 만난경우를 가려줌

        visit = [[False]*W for _ in range(H)] # 방문배열

        while s_row < H-1 and not meet: # 폭탄이 끝까지 갔거나 벽돌을 만난 경우에 while문 종료
            s_row += 1 # 폭탄을 밑으로 쭈욱 보내준다.
            if temp[s_row][j]: # 만약 벽돌을 만나면
                meet = True # 만났고
                stack = deque()
                stack.append([s_row,j]) # 이 첫 벽돌을 기점으로 연쇄적으로 폭탄 터트려 줄거임
                visit[s_row][j] = True # 방문 배열 체크

                while stack: # 터트릴 벽돌이 남아있는 경우 계속 반복
                    row, col = stack.popleft()
                    k = copy.deepcopy(temp[row][col]) # 폭탄의 폭발 범위를 저장
                    temp[row][col] = 0 # 폭파된 녀석은 0으로 갱신
                    for r in range(row-(k-1),row+k): # 범위만큼 폭파시킴
                        if 0<=r<H and not visit[r][col] and temp[r][col]: # 맵의 범위안에 있거나 아직 방문을 안했거나 벽돌이 존재하는 경우
                            stack.append([r,col]) # 폭파시켜줄 벽돌로 stack 넣어줌.
                            visit[r][col] = True # 방문 체크
                    for c in range(col-(k-1),col+k):
                        if 0<=c<W and not visit[row][c] and temp[row][c]:
                            stack.append([row,c])
                            visit[row][c] = True

                for j in range(W): # 한번의 폭파 단위로, 한번의 연쇄폭파 종료 후 벽돌을 떨어트려줌.
                    gravity_temp = []
                    for i in range(H):
                        if temp[i][j]:
                            gravity_temp.append(temp[i][j])
                            temp[i][j] = 0
                    for a in range(len(gravity_temp)):
                        temp[H-len(gravity_temp)+a][j] = gravity_temp[a]

                bfs(copy.deepcopy(temp), cnt+1) # 한번 터트렸으면 cnt를 증가시켜 다시 폭파 진행


for tc in range(1,int(input())+1):
    N, W, H = map(int, input().split()) # 구슬 발포 횟수, 배열의 넓이와 높이를 받아준다.
    arr = [list(map(int, input().split())) for _ in range(H)]
    # 배열 정보를 받아주고
    ans = 0xffffffff
    # 최대로 벽돌을 깼을때 남아있는 최소 벽돌의 개수를 갱신시켜 줄거임

    bfs(copy.deepcopy(arr), 0) # 넓이우선탐색으로 모든 경우의 수를 파악해 문제를 풀어줄거다.
    print("#{} {}".format(tc, ans))
```

- 이때부터는 문제를 풀때 가급적이면 주석을 달아 보도록 노력하자 결심했다.
- 시간이 지나 다시 본 코드를 이해해 설명을 쓰기는 쉽지 않기 때문도 있고, 주석을 달며 더 코드의 흐름에 대한 이해도가 깊어질 수 있기 때문이다.

