# swea

# 최대상금

### 일자 20201029

#### 문제

퀴즈 대회에 참가해서 우승을 하게 되면 보너스 상금을 획득할 수 있는 기회를 부여받는다.

우승자는 주어진 숫자판들 중에 두 개를 선택에서 정해진 횟수만큼 서로의 자리를 위치를 교환할 수 있다.

예를 들어, 다음 그림과 3, 2, 8, 8, 8 의 5개의 숫자판들이 주어지고 교환 횟수는 2회라고 하자.

교환전>

![img](https://swexpertacademy.com/main/common/fileDownload.do?downloadType=CKEditorImages&fileId=AV2XbrHKDgMBBASl)

처음에는 첫번째 숫자판의 3과 네 번째 숫자판의 8을 교환해서 8, 2, 8, 3, 8이 되었다.
 
![img](https://swexpertacademy.com/main/common/fileDownload.do?downloadType=CKEditorImages&fileId=AV2Xbt6KDgQBBASl)

다음으로, 두 번째 숫자판 2와 마지막에 있는 8을 교환해서 8, 8, 8, 3, 2이 되었다.

![img](https://swexpertacademy.com/main/common/fileDownload.do?downloadType=CKEditorImages&fileId=AV2XbwhKDgUBBASl)

정해진 횟수만큼 교환이 끝나면 숫자판의 위치에 부여된 가중치에 의해 상금이 계산된다.

숫자판의 오른쪽 끝에서부터 1원이고 왼쪽으로 한자리씩 갈수록 10의 배수만큼 커진다.

위의 예에서와 같이 최종적으로 숫자판들이 8,8,8,3,2의 순서가 되면 88832원의 보너스 상금을 획득한다.

여기서 주의할 것은 반드시 횟수만큼 교환이 이루어져야 하고 동일한 위치의 교환이 중복되어도 된다.

다음과 같은 경우 1회의 교환 횟수가 주어졌을 때 반드시 1회 교환을 수행하므로 결과값은 49가 된다.

![img](https://swexpertacademy.com/main/common/fileDownload.do?downloadType=CKEditorImages&fileId=AV2XbzSaDgYBBASl)

94의 경우 2회 교환하게 되면 원래의 94가 된다.

정해진 횟수만큼 숫자판을 교환했을 때 받을 수 있는 가장 큰 금액을 계산해보자.

**[입력]**

가장 첫 줄은 전체 테스트 케이스의 수이다.

최대 20개의 테스트 케이스가 표준 입력을 통하여 주어진다.

각 테스트 케이스에는 숫자판의 정보와 교환 횟수가 주어진다.

숫자판의 정보는 정수형 숫자로 주어지고 **최대 자릿수**는 6자리이며, **최대 교환 횟수**는 10번이다.

**[출력]**

각 테스트 케이스마다, 첫 줄에는 “#C”를 출력해야 하는데 C는 케이스 번호이다.

같은 줄에 빈 칸을 하나 사이에 두고 교환 후 받을 수 있는 가장 큰 금액을 출력한다.

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