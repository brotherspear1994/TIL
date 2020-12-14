# swea

# 러시아 국기 같은 깃발

### 일자 20200904

### 문제

[본문 링크 참조](https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AWQl9TIK8qoDFAXj&categoryId=AWQl9TIK8qoDFAXj&categoryType=CODE)

2016년은 삼성전자가 러시아 현지법인을 설립한지 20주년이 된 해이다. 이를 기념해서 당신은 러시아 국기를 만들기로 했다.

먼저 창고에서 오래된 깃발을 꺼내왔다. 이 깃발은 N행 M열로 나뉘어 있고, 각 칸은 흰색, 파란색, 빨간색 중 하나로 칠해져 있다.

당신은 몇 개의 칸에 있는 색을 다시 칠해서 이 깃발을 러시아 국기처럼 만들려고 한다. 다음의 조건을 만족해야 한다.

- 위에서 몇 줄(한 줄 이상)은 모두 흰색으로 칠해져 있어야 한다.
- 다음 몇 줄(한 줄 이상)은 모두 파란색으로 칠해져 있어야 한다.
- 나머지 줄(한 줄 이상)은 모두 빨간색으로 칠해져 있어야 한다.


이렇게 러시아 국기 같은 깃발을 만들기 위해서 새로 칠해야 하는 칸의 개수의 최솟값을 구하여라.

**[입력]**

첫 번째 줄에 테스트 케이스의 수 T가 주어진다.

각 테스트 케이스의 첫 번째 줄에는 두 정수 N,M(3≤N,M≤50)이 공백으로 구분되어 주어진다.

다음 N개의 줄에는 M개의 문자로 이루어진 문자열이 주어진다. i번 째 줄의 j번째 문자는 깃발에서 i번째 행 j번째 열인 칸의 색을 의미한다.

‘W’는 흰색, ‘B’는 파란색, ‘R’은 빨간색을 의미한다. ‘W’, ‘B’, ‘R’외의 다른 문자는 입력되지 않는다.


**[출력]**

각 줄마다 "#T" (T는 테스트 케이스 번호)를 출력한 뒤, 러시아 국기 같은 깃발을 만들기 위해서 새로 칠해야 하는 칸의 개수의 최솟값을 구하여 T 줄에 걸쳐서 출력한다.




#### 풀이1

```python
T = int(input())
for tc in range(1,T+1):
    N, M = map(int,input().split())
    flag = [list(input()) for _ in range(N)]
    Min = 987654321
    wcount = 0
    for w in range(0,N-2):
        for i in range(M):
            if flag[w][i] != 'W': wcount+=1
        bcount = 0
        for b in range(w+1,N-1):
            for j in range(M):
                if flag[b][j] != 'B': bcount += 1
            rcount = 0
            for r in range(b+1,N):
                for k in range(M):
                    if flag[r][k] != 'R': rcount += 1
            count = wcount + bcount + rcount
            if Min > count: Min = count

    print ("#{} {}".format(tc, Min))
```



#### 풀이2

```python
for tc in range(1,int(input())+1):
    N,M = map(int,input().split())
    W = [0]*N
    B = [0]*N
    R = [0]*N
    for i in range(N):
        arr = input()
        W[i] = arr.count("W")
        B[i] = arr.count("B")
        R[i] = M - W[i] - B[i]
    for i in range(1,N):
        W[i] += W[i-1]
        B[i] += B[i-1]
        R[i] += R[i-1]
    ans = N*M
    for i in range(N-2): # 흰색이 한줄을 가져야 하므로
        for j in range(i+1,N-1): # 마지막 한줄을 남겨야함
            cnt = M * (i+1) - W[i]
            cnt += M*(j-i) - (B[j]-B[i])
            cnt += M*(N-1-j)-(R[N-1]-R[j])
            ans = min(ans,cnt)
    print("#{} {}".format(tc, ans))
```

- 당시에는 꽤 어려웠던 문제로 기억한다.
- 수리적인 경우의 수를 나누어, for문을 이용해 칠해야 하는 칸의 개수의 최소값을 구해내야 한다.
- 알고리즘 보다는 수학적 사고가 더 중요한 문제이다. 이런 유형의 문제는 아무리 알고리즘을 잘한다 해도 생각을 하지 않으면 쉽게 풀지 못한다는 것을 느꼈다.