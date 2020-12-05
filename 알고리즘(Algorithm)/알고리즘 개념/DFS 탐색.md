# DFS 탐색

[TOC]

### DFS 탐색 알고리즘 코드

```python
'''
7
0110100
0110101
1110101
0000111
0100000
0111110
0111000
'''

dr = [-1,0,1,0]
dc = [0,1,0,-1]

def dfs(r,c): # 현재 좌표
    arr[r][c] = 2
    for k in range(4):
        nr = r + dr[k]
        nc = c + dc[k]
        if nr < 0 and nr >= N or nc < 0 and nc >= N: continue
        if arr[nr][nc] == 0 or arr[nr][nc] ==2: continue
        dfs(nr,nc)



N = int(input())
arr = [list(map(int, input())) for _ in range(N)]
# for row in arr:
#     print(row)
for i in range(N):
    for j in range(N):
        if arr[i][j] == 1:
            dfs(i,j)  # dfs탐색 시작
for row in arr:
    print(row)
```

- 배열이 주어졌을 때 1이 적힌 숫자를 깊이 우선 탐색(dfs)로 전부 탐색하며 2로 전환시키는 알고리즘을 구현해 보는 시간을 가졌다.
- 이동은 사방탐색을 통해 실시하였다.
