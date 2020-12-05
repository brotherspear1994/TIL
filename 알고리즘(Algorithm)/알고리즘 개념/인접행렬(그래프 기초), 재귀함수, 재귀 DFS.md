# 인접행렬 & 재귀함수 & 재귀 DFS

[TOC]

### 인접행렬 기초

```python
'''
7 8
1 2 1 3 2 4 2 5 4 6 5 6 6 7 3 7
'''
V,E = map(int,input().split())
# 인접행렬 생성
adj = [[0] * (V+1) for _ in range(V+1)]

edges = list(map(int, input().split()))
for i in range(E):
    n1, n2 = edges[i*2], edges[i*2+1]
    adj[n1][n2] = 1
    adj[n2][n1] = 1
# for row in adj:
#     print(row)

```

- 인접행렬을 만드는 법의 기초를 익혀보았다.
- 이미 인접리스트와 인접행렬을 만들줄 알지만 github에 commit을 남기며 다시금 되돌아 보는 좋은 시간이 됐다.

### 재귀함수 기초

```python
# 재귀함수

# def func():
#     print("hello")
#     func()
#
# func()

# 위 코드를 그대로 실행하면 무한 반복 발생

'''
무한 반복에 빠지지 않게하려면??
    매개변수를 하나 받음
    재귀 호출이 발생할때마다 매개변수의 값이 변하도록 설정
    재귀 함수에서 매개변수의 값을 이용해서 조건을 설정하고 일정조건을 만족하면 리턴하도록 설정
'''

# hello 5번만 출력
def func(num):
    i = num
    print("hello")
    i -= 1
    if i > 0: return func(i)
    else: return


func(5)

def fun(k):
    if k < 0:
        return
    else:
        print("hello")
        fun(k-1)
fun(5)

def pita(k):
    if k < 1:
        return
    elif k == 1:
        return 1
    else:
        return k + pita(k-1)

print(pita(10))

# 선생님 풀이
def sum(k, total):
    if k <= 0:
        print(total)
        return
    # print(k)
    sum(k-1,total+k)

sum(10,0)

def sum2(k):
    if k == 0:
        return 0
    return k + sum2(k-1)

print(sum2(10))

# 연습
def sum3(k, total):
    if k == 0:
        print(total)
        return
    else:
        sum3(k-1, k+total)

sum3(10,0)
```



### 재귀 DFS

```python
'''
7 8
1 2 1 3 2 4 2 5 4 6 5 6 6 7 3 7
'''
def dfs(v):
    visited[v] = 1
    print(v, end=" ")
    for w in range(1, N+1):
        if G[v][w] == 1 and visited[w] == 0:
            dfs(w)

# 정점, 간선
N, E = map(int, input().split())
# 간선들
temp = list(map(int,input().split()))
#인접행렬
G = [[0] * (N+1) for _ in range(N+1)]
#방문체크
visited = [0] * (N+1)
#간선들을 인접행렬에 입력 저장
for i in range(E):
    s, e = temp[2*i], temp[2*i+1]
    G[s][e] = 1
    G[e][s] = 1
# for row in G:
#     print(row)

dfs(1)

# def dfs(v):
#     visited[v] = 1
#     print(v, end=' ')
#     for w in range(N+1):
#         if G[v][w] == 1 and visited[w] == 0:
#             dfs(w)
# 
# 
# N, M = map(int, input().split())
# 
# G = [[0] * (N+1) for _ in range(N+1)]
# # print(G)
# visited = [0] * (N+1)
# lst = list(map(int, input().split()))
# for i in range(M):
#     s = lst[2*i]
#     e = lst[(2*i)+1]
#     G[s][e] = 1
#     G[e][s] = 1
# # print(G)
# 
# dfs(1)

```

- 재귀 함수의 기초 개념 학습 후 직접 연습을 가져보는 시간을 가졌다.
- 이후 깊이우선 탐색을 스택이 아닌 재귀함수를 이용하는 법을 학습했다. 
- 지금은 재귀함수를 활용이 익숙하고, 한발 더 나아가 재귀함수의 활용만큼 백트랙킹도 중요하다는 사실을 잘 알지만, 당시에는 나에게 매우 생소하게 다가온것으로 기억난다.