# swea

# 보급로

### 일자 20201106

### 문제

[본문 링크 참조](https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AV15QRX6APsCFAYD&categoryId=AV15QRX6APsCFAYD&categoryType=CODE)

#### 풀이

```python
from collections import deque

dx = [-1,0,1,0]
dy = [0,-1,0,1]

def dijkstra():
    Q = deque()
    Q.append((0,0,key[0][0]))
    while Q:
        x, y, w = Q.popleft()
        for k in range(4):
            nx = x + dx[k]
            ny = y + dy[k]
            if 0 <= nx < N and 0 <= ny < N:
                if key[nx][ny] > key[x][y] + arr[nx][ny]:
                    key[nx][ny] = key[x][y] + arr[nx][ny]
                    Q.append((nx, ny, key[x][y] + arr[nx][ny]))
    return key[-1][-1]


for tc in range(1,int(input())+1):
    N = int(input())
    arr = [list(map(int,input())) for _ in range(N)]
    # for row in arr:
    #     print(row)
    # print()
    INF = 0xfffff
    key = [[INF]*N for _ in range(N)]
    key[0][0] = 0

    print("#{} {}".format(tc, dijkstra()))
```

- 이 때는 MST Prim과 Dikjkstra를 잘 파악하고 있어서, 해당 유형의 문제가 나오면 공식 대입하듯 뚝딱 풀어냈다.