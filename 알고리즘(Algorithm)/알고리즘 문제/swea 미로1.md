# swea

# 미로1

### 일자 20201020

### 문제

[본문링크 참조](https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AV14vXUqAGMCFAYD&categoryId=AV14vXUqAGMCFAYD&categoryType=CODE)

#### 풀이

```python
dr = [-1,0,1,0]
dc = [0,-1,0,1]
def dfs(r, c):
    global ans
    maze[r][c] = 1
    for k in range(4):
        nr = r + dr[k]
        nc = c + dc[k]
        if 0 <= nr < 16 and 0 <= nc < 16 and maze[nr][nc] == 0:
            dfs(nr, nc)
        elif 0 <= nr < 16 and 0 <= nc < 16 and maze[nr][nc] == 3:
            ans = 1
            return

for tc in range(1, 11):
    TC = int(input())
    maze = [list(map(int, input())) for _ in range(16)]
    ans = 0
    dfs(1, 1)
    print("#%d" % tc, ans)
```

- 앞서 이전에 풀었던 미로 문제와 매우 유사하나 다른 문제이다.
