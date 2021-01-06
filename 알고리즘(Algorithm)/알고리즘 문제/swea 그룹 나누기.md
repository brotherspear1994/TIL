# swea

# 그룹 나누기

### 일자 20201107

### 문제

수업에서 같은 조에 참여하고 싶은 사람끼리 두 사람의 출석 번호를 종이에 적어 제출하였다.

한 조의 인원에 제한을 두지 않았기 때문에, 한 사람이 여러 장의 종이를 제출하거나 여러 사람이 한 사람을 지목한 경우 모두 같은 조가 된다.

예를 들어 1번-2번, 1번-3번이 같은 조가 되고 싶다고 하면, 1-2-3번이 같은 조가 된다. 번호를 적지도 않고 다른 사람에게 지목되지도 않은 사람은 단독으로 조를 구성하게 된다.

1번부터 N번까지의 출석번호가 있고, M 장의 신청서가 제출되었을 때 전체 몇 개의 조가 만들어지는지 출력하는 프로그램을 만드시오.


**[입력]**

첫 줄에 테스트 케이스의 개수가 주어지고, 다음 줄부터 테스트 케이스 별로 첫 줄에 N과 M, 다음 줄에 M 쌍의 번호가 주어진다. 2<=N<=100, 1<=M<=100

**[출력]**

각 줄마다 "#T" (T는 테스트 케이스 번호)를 출력한 뒤, 답을 출력한다.

#### 풀이1

```python
def find_set(x):
    if x != p[x]:
        p[x] = find_set(p[x])
    return p[x]

def union(x,y):
    p[find_set(y)] = find_set(x)

for tc in range(1, int(input())+1):
    N, M = map(int, input().split())
    edges = list(map(int, input().split()))
    p = list(range(N+1))

    for i in range(M):
        a, b = edges[i*2], edges[i*2+1]
        union(a,b)

    for i in range(1,N+1):
        find_set(i)

    ans = len(set(p))-1
    print("#{} {}".format(tc, ans))
```

- 문제를 보고 find, union 을 구현해보라 하는 것 같아 복습 및 응용겸 굳이 find_set과 union을 직접 만들어 풀어보았다.

#### 풀이2

```python
def bfs(v):
    visit[v] = 1
    Q = [v]
    while Q:
        row = Q.pop(0)
        for w in range(1, N+1):
            if not visit[w] and adj[row][w]:
                visit[w] = True
                Q.append(w)

for tc in range(1,int(input())+1):
    N, M = map(int, input().split())
    visit = [False]*(N+1)

    adj = [[0]*(N+1) for _ in range(N+1)]
    info = list(map(int,input().split()))
    for i in range(M):
        a, b = info[i*2], info[i*2+1]
        adj[a][b] = 1
        adj[b][a] = 1

    ans = 0
    for i in range(1,N+1):
        if not visit[i]:
            bfs(i)
            ans += 1
    print("#{} {}".format(tc, ans))
```

- 풀이2는 교수님 것인데, 교수님은 굳이 find_set과 union 알고리즘을 사용하시지는 않았다...

