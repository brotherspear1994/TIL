# swea

# 배열 최소 합

### 일자 20200901



### 문제

NxN 배열에 숫자가 들어있다. 한 줄에서 하나씩 N개의 숫자를 골라 합이 최소가 되도록 하려고 한다. 단, 세로로 같은 줄에서 두 개 이상의 숫자를 고를 수 없다.

조건에 맞게 숫자를 골랐을 때의 최소 합을 출력하는 프로그램을 만드시오.
 

예를 들어 다음과 같이 배열이 주어진다.
 

| 2    | 1    | 2    |
| ---- | ---- | ---- |
| 5    | 8    | 5    |
| 7    | 2    | 2    |



이경우 1, 5, 2를 고르면 합이 8로 최소가 된다.

 

**[입력]**
 

첫 줄에 테스트 케이스 개수 T가 주어진다. 1≤T≤50
 

다음 줄부터 테스트 케이스의 첫 줄에 숫자 N이 주어지고, 이후 N개씩 N줄에 걸쳐 10보다 작은 자연수가 주어진다. 3≤N≤10

 

**[출력]**
 

각 줄마다 "#T" (T는 테스트 케이스 번호)를 출력한 뒤, 합계를 출력한다.



#### 풀이1

```python
'''
3
3
2 1 2
5 8 5
7 2 2
3
9 4 7
8 6 5
5 3 7
5
5 2 1 1 9
3 3 8 3 1
9 2 8 8 6
1 5 7 8 3
5 5 4 6 8
'''
def subset(y):
    global min_sub, min_final

    if min_final < min_sub: return

    if y==N:
        if min_sub < min_final:
            min_final = min_sub
        return

    for x in range(N):
        if not bit[x]:
            bit[x] = 1
            min_sub += arr[y][x]
            subset(y+1)
            bit[x] = 0
            min_sub -= arr[y][x]

for tc in range(1,int(input())+1):
    N = int(input())
    arr = [list(map(int,input().split())) for _ in range(N)]
    # for row in arr:
    #     print(row)
    # print()
    bit = [0]*N
    min_sub, min_final = 0, 987654321
    subset(0)

    print("#{} {}".format(tc, min_final))
```



### 풀이2

```python
'''
3
3
2 1 2
5 8 5
7 2 2
3
9 4 7
8 6 5
5 3 7
5
5 2 1 1 9
3 3 8 3 1
9 2 8 8 6
1 5 7 8 3
5 5 4 6 8
'''
for tc in range(1,int(input())+1):
    N = int(input())
    arr = [list(map(int,input().split())) for _ in range(N)]
    # for row in arr:
    #     print(row)
    # print()
    bit = [0]*N
    min_sub, min_final = 0, 987654321

    while True:
        bit = [0] * N
        stack = []
        max_sub = 0
        k = 0
        for i in range(N):
            for j in range(N):
                if bit[i] == 0 and bit_second[j][i]==0:
                    stack.append(arr[j][i])
                    bit[i] = 1
                elif bit[i] == 1 or bit_second[j][i]: continue
        for num in stack:
            max_sub += num
        if max_sub > max_num: max_num = max_sub
            
            
    print("#{} {}".format(tc, min_final))

```

- 주어진 배열을 for문을 통해 탐색하며, 조건에 맞게 숫자를 골라 가능한 모든 경우의 수에서 최소합을 골라내는 문제이다.
- 해당 문제도 마찬가지로, 이전 문제들 처럼 재귀함수와 Stack(while문 Stack)을 이용해 두 가지 방식으로 풀어보았다.
- 가능하다면 다양한 방법의 풀이를 익혀보려고 노력하는 중이다.