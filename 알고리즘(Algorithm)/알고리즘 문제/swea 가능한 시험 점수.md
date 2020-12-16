# swea

# 가능한 시험 점수

### 일자 20200911

### 문제

영준이는 학생들의 시험을 위해 N개의 문제를 만들었다.

각 문제의 배점은 문제마다 다를 수 있고, 틀리면 0점 맞으면 배점만큼의 점수를 받게 된다.

학생들이 받을 수 있는 점수로 가능한 경우의 수는 몇 가지가 있을까?

예를 들어, 첫 번쨰 Testcase의 경우, 총 문제의 개수는 3개이며 각각의 배점은 2, 3, 5점이다

가능한 시험 점수의 경우의 수를 살펴보면 0, 2, 3, 5, 7, 8, 10의 7가지가 있다.

두 번째 Testcase의 경우, 총 문제의 개수는 10개이며 각각의 배점은 모두 1점이다.

가능한 시험점수의 경우의 수를 살펴보면 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10으로 모두 11가지이다.


**[입력]**

첫 번째 줄에 테스트 케이스의 수 T가 주어진다.

각 테스트 케이스의 첫 번째 줄에는 자연수 N(1 ≤ N ≤ 100)이 주어진다.

두 번째 줄에는 각 문제의 배점을 의미하는 N개의 자연수가 공백으로 구분되어 주어진다. 배점은 1이상 100이하의 자연수이다.

**[출력]**

각 테스트 케이스마다 학생들이 받을 수 있는 점수의 경우의 수를 출력한다.

#### 풀이1

```python
########## dfs 풀이#############
T = int(input())
for tc in range(1,T+1):
    N = int(input())
    score = list(map(int,input().split()))
    # print(score)
    visit = [0]*(sum(score)+1) # 마지막에 중복을 제거
    def dfs(k,s):
        if k == N:
            # print(s,end=' ')
            visit[s] = 1
            print(visit)
        else:
            dfs(k+1,s) # k 번문제를 틀린경우
            dfs(k+1,s+score[k])
    dfs(0,0)
    print("#{} {}".format(tc, sum(visit)))
```

#### 풀이2

```python
######### dfs 백트래킹 ################
T = int(input())
for tc in range(1,T+1):
    N = int(input())
    score = list(map(int,input().split()))
    # print(score)
    visit = [[0]*(sum(score)+1) for _ in range(N+1)]
    def dfs(k,s):
        if visit[k][s]: return
        visit[k][s] = 1
        if k == N: return
        dfs(k+1,s) # k 번문제를 틀린경우
        dfs(k+1,s+score[k])
    dfs(0,0)
    print(sum(visit[N]))
```

#### 풀이3

```python
# #############bfs 풀이 ##############
T = int(input())
for tc in range(1,T+1):
    N = int(input())
    score = list(map(int,input().split()))
    # print(score)
    visit = [0]*(sum(score)+1)
    Q = [[0,0]] # k, s
    while Q:
        k,s = Q.pop(0)
        if k == N:
            print(s, end=' ')
            visit[s] = 1
        else:
            Q.append([k+1,s])
            Q.append([k+1,s+score[k]])
    print(sum(visit))
```

#### 풀이4

```python
# ############# bfs 백트래킹 #################
T = int(input())
for tc in range(1,T+1):
    N = int(input())
    score = list(map(int,input().split()))
    # print(score)
    visit = [0]*(sum(score)+1)
    Q = [0]
    for val in score:
        for i in range(len(Q)):
            if visit[Q[i]+val]: continue
            visit[Q[i]+val] = 1
            Q.append(Q[i]+val)
```

- 백트랙킹을 연습해볼 수 있었던 아주 좋은 문제였다.
- 백트랙킹은 코딩을 배운지 약 5개월쯤 된 나도 여전히 어려워 하는 부분이다.
- 앞으로도 꾸준히 프로그램 구동 시간을 줄일 수 있는 백트랙킹 연습을 해야겠다.

