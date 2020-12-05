# swea

# 최대 사각 테두리 합

### 일자 20200829~20200830

#### 풀이

```python
for tc in range(1,int(input())+1):
    N, M, K = map(int,input().split())
    arr = [list(map(int, input().split())) for _ in range(N)]
    # for row in arr:
    #     print(row)
    # print()

    max_area = 0
    area_sub = 0
    for j in range(M-K+1):
        for i in range(N-K+1):
            for g in range(K):
                for k in range(K):
                    if g == 0:
                        area_sub += arr[i+g][j+k]
                    elif g == K-1:
                        area_sub += arr[i+g][j+k]
                    else:
                        area_sub += (arr[i+g][j]+arr[i+g][j+K-1])
                        break
            if max_area < area_sub: max_area = area_sub
            area_sub = 0
    print("#{} {}".format(tc, max_area))
```

- SWEA 역량테스트 IM대비를 위해 시간이지나 까먹을 수 있는 부분들을  다시 한 번 풀며 복습해봤다.(0829기준)
- 정사각형의 한변의 길이가 주어질 때, 주어진 배열 중에서 정사각형의 최대 사각 테두리의 합을 구하는 문제이다.
- for문을 잘 활용할 수 있는지 물어보는 매우 기본적인 문제였다.

