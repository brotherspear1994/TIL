# swea

# 최대상금

### 일자 20201029

#### 문제

[본문 링크 참조](https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AV15Khn6AN0CFAYD&categoryId=AV15Khn6AN0CFAYD&categoryType=CODE)

#### 풀이 1

```python
def rotate(idx, K, times):
    global max_reward
    if times == K:
        if board[:] not in stack:
            stack.append(board[:])
        return
    else:
        for i in range(idx+1, len(board)):
            board[idx], board[i] = board[i], board[idx]
            if K == 2:
                for j in range(len(board) - 1):
                    rotate(j, K, times+1)
            elif K == 10:
                max_reward = 987645
            else:
                rotate(idx, K, times + 1)
            board[idx], board[i] = board[i], board[idx]
 
for tc in range(1,int(input())+1):
    info = list(map(int, input().split()))
    num_info, K = list(str(info[0])), info[1]
    board = []
    for i in num_info:
        board.append(int(i))
    # print(board)
    stack = []
    max_reward = 0
    for j in range(len(board)-1):
        rotate(j, K, 0)
    # print(tc, stack)
 
    for i in range(len(stack)):
        temp = 0
        for j in range(len(stack[i])):
            temp += stack[i][j]*(10**(len(stack[i])-1-j))
        if max_reward < temp: max_reward = temp
    print("#{} {}".format(tc, max_reward))
```



#### 풀이 2

```python
def swap(k):
    global ans
    num = int(''.join(map(str, arr)))
    if num in visit[k]: return
    else: visit[k].add(num)
    if k == cnt:
        if num > ans:
            ans = max(ans, num)
    else:
        for i in range(N-1):
            for j in range(i+1,N):
                arr[i], arr[j] = arr[j], arr[i]
                swap(k+1)
                arr[i], arr[j] = arr[j], arr[i]
 
 
for tc in range(1,int(input())+1):
    info = list(map(str,input().split()))
    cnt = int(info[1])
    arr = list(map(int,info[0]))
    # print(arr)
    N = len(arr)
    ans = 0
    visit = list(set() for _ in range(11))
 
    swap(0)
    print("#%d" % tc, ans)
```

- 내 풀이 방식과 교수님의 풀이 방식, 두가지 방식으로 풀어봤다.
- 내 풀이와 교수님의 풀이 방식이 큰 차이는 없지만, 백트랙킹의 위치를 놓는 부분이 교수님의 풀이법이 거의 정답과 가깝다. 내 방식의 백트래킹(가지치기)는 효율적으로 런타임을 줄일 수 없었다.
- 이 '최대상금' 문제를 통해 재귀함수를 실행할때 백트랙킹을 어떻게 해야하는지, 또 백트랙킹의 개념에 대해 좀더 깊이 느낄 수 있었다.
- 특히 특정 깊이를 기준으로 이후의 깊이에서 유망하지 않은 정답(혹은 불필요한 과정)은 가지치기를 해줌으로써 그 뒤의 과정에서는 비효율이 발생하지 않도록 하는 것이 포인트이다.