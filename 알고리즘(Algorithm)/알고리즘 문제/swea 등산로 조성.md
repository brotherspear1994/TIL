# swea

# 등산로 조성

### 일자 20201107

### 문제

[본문링크 참조](https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AV5PoOKKAPIDFAUq&categoryId=AV5PoOKKAPIDFAUq&categoryType=CODE)

#### 풀이

```python
import copy; from collections import deque

dx = [-1,0,1,0]
dy = [0,-1,0,1]

def bfs(x,y):
    max_dis = 0
    Q = deque()
    Q.append((x,y,1))
    while Q:
        x,y,dis = Q.popleft()
        max_dis = max(max_dis, dis)
        for k in range(4):
            nx = x + dx[k]
            ny = y + dy[k]
            if 0 <= nx < N and 0 <= ny < N and temp[x][y] > temp[nx][ny]:
                Q.append((nx,ny,dis+1))
    return max_dis


for tc in range(1,int(input())+1):
    N, K = map(int, input().split())
    arr = [list(map(int, input().split())) for _ in range(N)]
    height = 0
    for row in arr:
        height = max(height, max(row))

    ans = 0
    for k in range(K+1):
        for i in range(N):
            for j in range(N):
                temp = copy.deepcopy(arr)
                temp[i][j] = temp[i][j] - k
                for a in range(N):
                    for b in range(N):
                        if temp[a][b] == height:
                            ans = max(ans, bfs(a,b))

    print("#{} {}".format(tc, ans))
```

- 풀며 무언가를 느낀 문제이다.
- 처음에는 내가 정답에 해당하는 경우의 수를 직접 계산하며, 직접 알고리즘에 짜주려했었다.
- 하지만 문제를 풀며, 모든 가능한 경우의 수에 대해 다잌스트라를 실행해주면 훨씬 쉽게 풀릴 수 있다는 사실을 깨닳았다.
- 이 문제를 깊은 고민을 하며 푼 덕에, 이와 비슷한 유형의 문제는 바로바로 풀어낼 수 있게 됐다.
