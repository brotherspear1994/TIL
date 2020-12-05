# swea

# 델타검색

### 일자 20200805

#### 풀이

```python
arr =[[1,2,3,4],
      [5,6,7,8],
      [9,10,11,12]
      ]

N = len(arr)
M = len(arr[0])

dx = [0, 0, -1, 1]
dy = [-1, 1, 0, 0]


for x in range(N):
    for y in range(M):
        for i in range(4):
            testX = x + dx[i]
            testY = y + dy[i]
            if testX >= 0 and testX < N and testY >=0 and testY < M:
                print(arr[testX][testY], end=" ")
        print()
    print()
```



```py
import sys
sys.stdin = open('input (2).txt', 'r')

arr = [list(map(int, input().split())) for _ in range(5)]
#델타: 위, 오른쪽, 아래, 왼쪽
dr = [-1,0,1,0]
dc = [0,1,0,-1]

for i in range(len(arr)):
    # print(arr[i])
    for j in range(len(arr[i])):
        sum = 0
        for k in range(4):
            nr = i + dr[k]
            nc = j + dc[k]

            if nr < 0 or nr >= len(arr) or nc < 0 or nc >= len(arr):
                continue
            sum += abs(arr[i][j]-arr[nr][nc])
        print(sum, end= ' ')
    print()
```



- 델타 검색을 하는 법을 처음 익힌 시기였다.
- 코딩을 배운지 3개월 남짓된 요즘은, 주어진 문제를 바탕으로 델타검색을 원하는 방향과 순서대로 자유롭게 할 수 있지만 당시에는 익숙치 않아 꽤 어려운 개념이었다.