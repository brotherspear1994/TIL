# swea

# 파리퇴치

### 일자 20200806

### 문제

N x N 배열 안의 숫자는 해당 영역에 존재하는 파리의 개수를 의미한다.

아래는 N=5 의 예이다.
 

![img](swea 파리퇴치.assets/fileDownload.do)


M x M 크기의 파리채를 한 번 내리쳐 최대한 많은 파리를 죽이고자 한다.

죽은 파리의 개수를 구하라!

예를 들어 M=2 일 경우 위 예제의 정답은 49마리가 된다.
 

![img](swea 파리퇴치.assets/fileDownload.do)



**[제약 사항]**

\1. N 은 5 이상 15 이하이다.

\2. M은 2 이상 N 이하이다.

\3. 각 영역의 파리 갯수는 30 이하 이다.


**[입력]**

가장 첫 줄에는 테스트 케이스의 개수 T가 주어지고, 그 아래로 각 테스트 케이스가 주어진다.

각 테스트 케이스의 첫 번째 줄에 N 과 M 이 주어지고,

다음 N 줄에 걸쳐 N x N 배열이 주어진다.


**[출력]**

출력의 각 줄은 '#t'로 시작하고, 공백을 한 칸 둔 다음 정답을 출력한다.

(t는 테스트 케이스의 번호를 의미하며 1부터 시작한다.)



### 풀이 1

```python
import sys
sys.stdin = open("input (2).txt", "r")
T = int(input())
for tc in range(1,T+1):
    N,M = map(int,input().split())
    flies = [list(map(int, input().split())) for _ in range(N)]
    # print(flies)
    result = -1
    for r in range(N-M+1):
        for c in range(N-M+1):
            result_sub = 0
            for dr in range(M):
                for dc in range(M):
                    result_sub += flies[r+dr][c+dc]
            if result_sub > result:
                result = result_sub
    print("#{} {}".format(tc, result))
```

- for문 초급~중급 정도의 문제인것 같다.
- 배열의 모든 요소를 돌며 그 요소를 기준으로 특정한 범위(위에서는 주어진 M)의 파리를 잡았을때 가장 많은 파리를 잡을 수 있는 파리의 수를 구하는 문제이다.
- 얼마나 for문을 잘 활용할 수 있는지를 보며, 4중 for문을 돌리면 매우 쉽게 풀 수 있는 문제이다.



### 풀이 2

```python
T = int(input())
for tc in range(1,T+1):
    N, M = map(int,input().split())
    arr = [list(map(int,input().split())) for _ in range(N)]
    # for row in arr:
    #     print(row)
    max_get = 0
    max_sub = 0
    for i in range(0,N-M+1):
        for j in range(0,N-M+1):
            for a in range(M):
                for b in range(M):
                    max_sub += arr[i+a][j+b]
            if max_get < max_sub:
                max_get = max_sub
            max_sub = 0
    print("#{} {}".format(tc, max_get))
```

- SWEA 역량테스트 IM대비를 위해 시간이지나 까먹을 수 있는 부분들을  다시 한 번 풀며 복습해봤다.(0829기준)
- 한 달 간격의 차이로 똑같은 문제를 풀었지만, 파리퇴치 문제 같은 경우는 지금 두 코드를 비교해보니 크게 풀이 차이가 나지는 않았다.