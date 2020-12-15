# swea

# 작업순서

### 일자 20200908

### 문제

[본문 링크 참조](https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AV18TrIqIwUCFAZN&categoryId=AV18TrIqIwUCFAZN&categoryType=CODE)


#### 풀이1

```python
for tc in range(1,11):
    V, E = map(int,input().split())
    Gansun = list(map(int,input().split()))
    arr = [[0 for _ in range(V+1)] for _ in range(V+1)]
    for i in range(E):
        arr[Gansun[2*i]][Gansun[2*i+1]] = 1
    # if tc in range(1,5):
    #     for row in arr:
    #         print(row)
    stack = []
    start_stack = []
    for i in range(1,V+1):
        sero_start = 0
        for j in range(1,V+1):
            sero_start += arr[j][i]
        if sero_start == 0:
            start_stack.append(i)

    while start_stack:
        col = start_stack.pop(0)
        sero = 0
        for j in range(1,V+1):
            sero += arr[j][col]
        if sero == 0 and col not in stack:
            stack.append(col)
            for k in range(1,V+1):
                arr[col][k] = 0
        for a in range(1,V+1):
            sero_sub = 0
            for b in range(1,V+1):
                sero_sub += arr[b][a]
            if sero_sub == 0 and a not in start_stack and a not in stack:
                start_stack.append(a)
    print("#{}".format(tc),end=' ')
    for element in stack:
        print(element, end= ' ')
    print()
```



### 풀이 2

```python
def dfs(v): #현재 정점 : v
    visited[v] = True
    for n in adj[v]:
        if not visited[n]:
            dfs(n)
    S.append(v)
    print(visited)
    print(S)

for tc in range(1,1+1):
    V,E = map(int,input().split())
    edges = list(map(int,input().split()))
    adj = [[] for i in range(V+1)]    #인접리스트 생성
    visited = [False] * (V+1)   #방문배열
    indeg = [0] *(V+1)  #각 정점의 진입차수 저장
    S = []  #방문한 정점 저장
    for i in range(0,E):
        u,v = edges[i*2],edges[i*2+1]   #시작 정점 , 끝정점
        adj[u].append(v)    #유향그래프 -> 시작->끝만 표현
        indeg[v] +=1    #끝 정점의 진입차수 증가시킴
    print(adj)
    for i in range(1,V+1):  #정점을 순회함
        if indeg[i]: continue   #해당정점에 진입차수가 있으면 순회 안함
        dfs(i)      #아니라면 => 미리 처리할 작업이 없음
    print("#{}".format(tc), end=" ")
    print(*S[::-1])
```
