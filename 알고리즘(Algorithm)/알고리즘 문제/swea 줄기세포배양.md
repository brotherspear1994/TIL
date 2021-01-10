# swea

# 줄기세포배양

### 일자 20201203

### 문제

[본문 링크 참조](https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AWXRJ8EKe48DFAUo&categoryId=AWXRJ8EKe48DFAUo&categoryType=CODE)

#### 풀이

```python
import sys; sys.stdin = open('줄기세포.txt', 'r')

# 한번에 통과해서 당황함,,,,ㄷㄷ
# 시뮬레이션을 정식으로 배운적이 없어(수업시간에도 따로 수업이 없었다) 시뮬레이션을 풀때마다 나만의 방식을 고안해냈는데,
# 나(이형창)는 이것을 '인접행렬 스택'이라고 명명했다.
# 보통 인접행렬 스택을 사용한 문제들은 런타임 에러가 지금까지 한번도 걸린적이 없다..! 배열을 모두 만들어도 이를 직접 전부 순회할 필요가 없이
# 좌표 정보도 인접행렬 스택에 담아 바로바로 지정해서 사용해주기 때문!

import copy

# 세포 번식은 네방향으로 이루어지므로 사방탐색용 dr, dc를 설정
dr = [-1,0,1,0]
dc = [0,-1,0,1]

for tc in range(1, int(input())+1):
    N, M, K = map(int, input().split()) # 각각 세로크기, 가로크기, 배양시간을 입력받음.
    arr = [[0]*(M+2*K) for _ in range(K)]+[[0]*K+list(map(int,input().split()))+[0]*K for _ in range(N)]+[[0]*(M+2*K) for _ in range(K)]
    # 1시간당 1칸씩 넓혀가므로 최대 K칸을 넓혀 갈 수 있으니 위와 같이 배열을 받을때 미리 맵을 추가적으로 그려줌.

    # 잘 입력받아졌나 확인.
    # if tc == 1:
    #     for row in arr:
    #         print(row)
    #     print()

    # 배열의 가로길이와 세로길이를 체크해서 정의
    arl = len(arr)
    for row in arr:
        acl = len(row)

    #번식할 세포들을 담을 stack과 비슷한 용도의 '인접행렬 스택'(나만의 방식)을 만들어줌.
    cell_list = []

    time_stmp = [[0]*acl for _ in range(arl)] # 세포가 번식된 시점의 시간을 입력해줄 time_stmp
    visit = [[False] * acl for _ in range(arl)] # 방문배열 만들어줌.

    # 이제 딱 한번만 전체를 순회하며 최초 세포를 cell_list에 담아줄거임
    for i in range(arl):
        for j in range(acl):
            if arr[i][j]:
                cell_list.append([i,j,arr[i][j],True]) #차례로 좌표정보, 생명력수치, 번식가능여부
                visit[i][j] = True # 담아줬으니 방문체크

    hours = 0

    while hours < K: # 시간만큼 while문을 돌리고
        cell_list.sort(reverse=True, key=lambda x: x[2])
        # 동시에 두개의 세포가 곂칠때 번식력이 강한 놈이 셀을 차지하므로, 처음부터 그냥 내림차순으로 정리해버린다.
        hours += 1 # 시간이 지났습니다. 세포들은 고개를 들어 움직여주세요.
        temp = copy.deepcopy(cell_list) # 딱 현재 cell_list에 담긴 세포개수만큼만 for문을 돌릴거다.
        for _ in range(len(temp)):
            r, c, exp, alive = cell_list.pop(0) #세포를 꺼내 정보들을 받고
            if (hours-time_stmp[r][c])/exp > 1 and alive:
                # 현재시각-세포가 생겨났을 당시 시각)/번식력이 1초과 2미만이면 번식은 가능하나 아직 죽지는 않는놈, 2이상이면 번식도 가능하면서(했거나 안했거나) 죽을놈, 1이하면 아직 번식 못하고 살아있는놈.
                for k in range(4): # 번식 가능한 놈이면 사방탐색실시
                    nr = r+dr[k]; nc = c+dc[k]
                    if not visit[nr][nc]: # 아직 세포가 없는 구역에 한하여 번식시작
                        arr[nr][nc] = exp
                        visit[nr][nc] = True
                        time_stmp[nr][nc] = hours
                        cell_list.append([nr,nc,exp,True])
            if 1 < (hours-time_stmp[r][c])/exp < 2: # 번식은 했지만 아직 살수있는놈
                cell_list.append([r,c,exp,False])
            elif (hours-time_stmp[r][c])/exp <= 1: # 번식도 아직 못한놈
                cell_list.append([r, c, exp, True])
            # 그 외 녀석들은 이미 번식하고 죽은 녀석들이기 때문에 cell_list에 넣어주지 않는다.
    print("#{} {}".format(tc, len(cell_list)))
```

- 시뮬레이션 유형의 문제를 풀 수 있는 실력까지 도달한 것 같다.
- 다만 문제를 푸는 시간이 다소 걸려 계속 연습하며 풀어봐야겠다.
