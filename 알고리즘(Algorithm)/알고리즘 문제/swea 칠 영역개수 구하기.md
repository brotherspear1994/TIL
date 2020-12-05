# swea

# 칠 영역개수 구하기

### 일자 20200829~20200830

#### 풀이

```python
'''
3
10 1
2 3 4 6
10 3
2 3 4 6
4 2 7 4
7 4 8 7
20 10
5 10 11 12
1 1 6 14
14 9 18 10
8 6 16 12
2 11 6 19
6 1 13 4
13 6 16 17
1 17 4 18
9 10 15 15
12 16 12 17
'''
for tc in range(1,int(input())+1):
    N, M = map(int, input().split())
    arr = [[0] * (N + 1) for _ in range(N + 1)]

    for _ in range(M):
        s_i, s_j, e_i, e_j = map(int, input().split())
        for i in range(s_i, e_i+1):
            for j in range(s_j, e_j+1):
                arr[i][j] = 1
    area = 0
    for i in range(N+1):
        for j in range(N+1):
            if arr[i][j] == 1: area += 1
    print("#{} {}".format(tc, area))

```

- SWEA 역량테스트 IM대비를 위해 시간이지나 까먹을 수 있는 부분들을  다시 한 번 풀며 복습해봤다.(0829기준)