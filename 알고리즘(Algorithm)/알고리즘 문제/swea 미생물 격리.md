# swea

# 미생물 격리

### 일자 20201203

### 문제

[본문 링크 참조](https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AV597vbqAH0DFAVl&categoryId=AV597vbqAH0DFAVl&categoryType=CODE)

#### 풀이

```python
# import sys; sys.stdin = open('미생물.txt', 'r')

for tc in range(1,int(input())+1):
    N, M, K = map(int, input().split())
    # 각각 셀의 개수, 격리 시간, 미생물 군집의 개수를 입력받는다.
    info = [] # 미생물 군집의 개수만큼 정보를 받아줄 info 빈 리스트 생성
    for _ in  range(K):
        row, col, num, dir = map(int, input().split())
        info.append([row,col,num,dir]) # 정보를 담아준다.
    # print(info)

    cnt = 0

    while cnt < M: # M시간에 걸쳐 미생물이 움직이고
        cnt += 1 # 시간을 체크
        for element in info: # 각각의 군집의 방향정보를 확인해서
            if element[3] == 1:
                element[0] -= 1 # 방향 정보에 따라 미생물을 이동시켜준다.
                if element[0] == 0 or element[0] == N-1 or element[1] == 0 or element[1] == N-1:
                    # 만약 미생물이 약품이 칠해진 구역에 도달한다면
                    element[2] = int(element[2]/2) # 미생물 수 절반으로 감소
                    element[3] = 2 # 방향 반대방향으로 바꿔주기.
            elif element[3] == 2:
                element[0] += 1
                if element[0] == 0 or element[0] == N-1 or element[1] == 0 or element[1] == N-1:
                    element[2] = int(element[2]/2)
                    element[3] = 1
            elif element[3] == 3:
                element[1] -= 1
                if element[0] == 0 or element[0] == N-1 or element[1] == 0 or element[1] == N-1:
                    element[2] = int(element[2]/2)
                    element[3] = 4
            elif element[3] == 4:
                element[1] += 1
                if element[0] == 0 or element[0] == N-1 or element[1] == 0 or element[1] == N-1:
                    element[2] = int(element[2]/2)
                    element[3] = 3
        info.sort(reverse=True, key=lambda x: x[2]) # 군집이 곂칠경우, 가장 마리수가 많은 군집을 따르므로, sort함수를 이용해 미생물 수 기준 내림차순
        # print(info)
        adj = [[[] for _ in range(N)] for _ in range(N)] # 방문배열의 역할을 해줄 adj
        for i in range(len(info)):
            r,c,n,d = info[i]
            if not adj[r][c]: # 아직 안 곂친다면 방문배열에 체크
                adj[r][c].extend([n,i])
            else:
                info[adj[r][c][1]][2] += n # 곂친다면 기존 군집에 추가시켜주기
                info[i][0], info[i][1], info[i][2], info[i][3] = 0, 0, 0, 0 # 합병된 군집은 정보 초기화

    result = 0
    for e in info: # 남은 미생물 수를 세주고 출력
        result += e[2]
    print("#{} {}".format(tc, result))



```

- 이때부터는 문제를 풀때 가급적이면 주석을 달아 보도록 노력하자 결심했다.
- 시간이 지나 다시 본 코드를 이해해 설명을 쓰기는 쉽지 않기 때문도 있고, 주석을 달며 더 코드의 흐름에 대한 이해도가 깊어질 수 있기 때문이다.

