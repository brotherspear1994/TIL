# swea

# 어디에 단어가 들어갈 수 있을까

### 일자 20200828

### 문제

[본문 링크 참조](https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AV5PuPq6AaQDFAUq&categoryId=AV5PuPq6AaQDFAUq&categoryType=CODE)

N X N 크기의 단어 퍼즐을 만들려고 한다. 입력으로 단어 퍼즐의 모양이 주어진다.

주어진 퍼즐 모양에서 특정 길이 K를 갖는 단어가 들어갈 수 있는 자리의 수를 출력하는 프로그램을 작성하라.


**[제약 사항]**

\1. N은 5 이상 15 이하의 정수이다. (5 ≤ N ≤ 15)

\2. K는 2 이상 N 이하의 정수이다. (2 ≤ K ≤ N)


**[입력]**

입력은 첫 줄에 총 테스트 케이스의 개수 T가 온다.

다음 줄부터 각 테스트 케이스가 주어진다.

테스트 케이스의 첫 번째 줄에는 단어 퍼즐의 가로, 세로 길이 N 과, 단어의 길이 K 가 주어진다.

테스트 케이스의 두 번째 줄부터 퍼즐의 모양이 2차원 정보로 주어진다.

퍼즐의 각 셀 중, 흰색 부분은 1, 검은색 부분은 0 으로 주어진다.


**[출력]**

테스트 케이스 t에 대한 결과는 “#t”을 찍고, 한 칸 띄고, 정답을 출력한다.

(t는 테스트 케이스의 번호를 의미하며 1부터 시작한다.)

#### 풀이1

```python
'''
1
5 3
0 0 1 1 1
1 1 1 1 0
0 0 1 0 0
0 1 1 1 1
1 1 1 0 1
'''
T = int(input())
for tc in range(1, T+1):
    N, k = map(int,input().split())
    # print(N, k)
    puzzle = [list(map(int,input().split())) for _ in range(N)]
    # for row in puzzle:
    #     print(row)

    stack = []
    cnt = 0
    # 가로 계산
    for i in range(N):
        for j in range(N):
            # push
            stack.append(puzzle[i][j])
            # print(stack)
            if stack[-1] == 0 and len(stack) <= k:
                stack = []
            elif stack[-1] == 0 and len(stack) == k+1:
                stack.pop()
                if len(stack) == k:
                    cnt += 1
                stack = []
            elif stack[-1] == 1 and len(stack) == k+1:
                stack = []
            elif stack[-1] == 1 and len(stack) == k and j == N-1:
                cnt += 1
        stack = []
    # print(cnt)

    # 세로 계산
    for i in range(N):
        for j in range(N):
            # push
            stack.append(puzzle[j][i])
            # print(stack)
            if stack[-1] == 0 and len(stack) <= k:
                stack = []
            elif stack[-1] == 0 and len(stack) == k + 1:
                stack.pop()
                if len(stack) == k:
                    cnt += 1
                stack = []
            elif stack[-1] == 1 and len(stack) == k + 1:
                stack = []
            elif stack[-1] == 1 and len(stack) == k and j == N - 1:
                cnt += 1
        stack = []
    print("#{} {}".format(tc, cnt))
```

- for문으로 배열을 순회하며 stack을 같이 활용해 특정 길이(K)를 갖는 퍼즐을 탐색하여 counting 해주면 풀 수 있는 문제이다.
- for문을 이용한 완전탐색이라고 할 수 있을 것 같다.
- 가로 길이와 세로 길이를 따로 탐색해주는 것이 포인트다.

### 풀이2

```python
T = int(input())
for tc in range(1,T+1):
    N,K = map(int,input().split())
    puzzle = [list(map(int,input().split())) for _ in range(N)]
    # for row in puzzle:
    #     print(row)
    dist = 0 # 자릿수

    for i in range(N): # 가로방향 검사
        words = 0 # 빈칸수
        cur = 0 # 현재위치
        while cur < N:
            if puzzle[i][cur] == 1: # 1일때 카운팅 시작
                words += 1
                if words == K and cur == N-1:
                    dist += 1
            else: # 0 일때
                if words == K:
                    dist += 1
                words = 0
            cur += 1

    for i in range(N): # 세로방향 검사
        words = 0 # 빈칸수
        cur = 0 # 현재위치
        while cur < N:
            if puzzle[cur][i] == 1: # 1일때 카운팅 시작
                words += 1
                if words == K and cur == N-1:
                    dist += 1
            else: # 0 일때
                if words == K:
                    dist += 1
                words = 0
            cur += 1
    print("{} {}".format(tc, dist))
```

- 맨 처음 문제를 푼 후 3일 정도지나 교수님의 풀이도 학습해봤다.
- 강의를 들으며 이해를 하고, 이후 개인시간에 혼자 코드를 안보고 짜보는 연습을 가졌다.
- 이번 풀이는 stack을 활용하지 않고 for문과 while문을 함께 사용해 푸는 방식이다.