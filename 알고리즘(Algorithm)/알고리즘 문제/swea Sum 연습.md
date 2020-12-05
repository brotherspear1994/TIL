# swea

# Sum

### 일자 20200805

#### 풀이

```python
import sys
sys.stdin = open("input (2).txt", "r")

#입력
TC = 10
for tc in range(1, TC+1):
    N = int(input())
    lst = []
    for i in range(100):
        sub_lst = list(map(int, input().split()))
        lst.append(sub_lst)
    # print(N)
    # print(lst)

    #계산
    # 각 행의 합

    sum_row_total = 0
    for a in range(100):
        sum_row = 0
        for b in lst[a]:
            sum_row += b
            if sum_row > sum_row_total:
                sum_row_total = sum_row
    # print(sum_row_total)

    sum_column_total = 0
    for b in range(100):
        sum_column = 0
        for a in range(100):
            sum_column += lst[a][b]
            if sum_column > sum_column_total:
                sum_column_total = sum_column
    # print(sum_column_total)

    sum_diagonal_1 = 0
    for a in range(100):
        for b in range(100):
            if a == b:
                sum_diagonal_1 += lst[a][b]
    # print(sum_diagonal_1)

    sum_diagonal_2 = 0
    for a in range(100):
        for b in range(99, -1, -1):
            if a+b == 99:
                sum_diagonal_2 += lst[a][b]
    # print(sum_diagonal_2)

    max_final = max([sum_row_total, sum_column_total, sum_diagonal_1, sum_diagonal_2])
    print("#{} {}".format(tc, max_final))
```

- 100 x 100 크기의 사각형(배열)이 주어졌을때, 각 행의합, 대각선의 합들을 계산해 가장 최대가 나오는 값을 구해보는 연습을 했다.
- for문을 이용해 배열을 내가 원하는데 자유롭게 탈 수 있는지 test 해보는 문제였다.