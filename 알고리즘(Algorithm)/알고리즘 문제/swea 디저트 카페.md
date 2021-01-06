# swea

# 디저트 카페

### 일자 20201107

### 문제

[본문 링크 참조](https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AV5VwAr6APYDFAWu&categoryId=AV5VwAr6APYDFAWu&categoryType=CODE)

#### 풀이

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

- 이 문제는 10월초에 맨처음 문제를 받고 풀지 못했다가, 11월에 다시 문제를 받고 해보니 풀어내는데 성공했다.
- 매우 뿌듯하다.