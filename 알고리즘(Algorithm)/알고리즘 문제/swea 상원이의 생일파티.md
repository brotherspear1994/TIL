# swea

# 상원이의 생일파티

### 일자 20201104

### 문제

상원이의 생일 파티가 곧 열린다!

그렇기에 상원이는 반 친구들에게 생일 파티 초대장을 주려고 한다.

그러나 파티가 어색하게 되는 것을 원치 않는 상원이는 모든 친구들에게 초대장을 줄 생각이 없다.

같은 반에 있지만, 서로 친한 친구가 아닐 수도 있기 때문이다.

상원이는 우선 자신과 친한 친구들에게는 모두 초대장을 주기로 했다.

여기에 더해서 친한 친구의 친한 친구인 경우에도 초대장을 주기로 했다.

총 몇 명의 친구들에게 초대장을 주어야 하는지 구하는 프로그램을 작성하라.

상원이의 반에는 N명이 있으며, 각 학생들은 1번에서 N번까지의 번호가 붙어 있다.

여기서 1번 학생이 상원이다.


**[입력]**

첫 번째 줄에 테스트 케이스의 수 T가 주어진다.

각 테스트 케이스의 첫 번째 줄에 두 정수 N, M ( 2 ≤ N ≤ 500, 1 ≤ M ≤ 104 ) 이 공백으로 구분되어 주어진다.

M은 친한 친구 관계의 수 이다.

다음 M개의 줄의 각 줄에는 두 정수 a, b (1 ≤ a ＜ b ≤ N) 이 주어진다.

이는 a번 학생과 b번 학생이 서로 친한 친구 관계에 있다는 의미이다.

**[출력]**

각 테스트 케이스마다 #T를 출력하고 한 칸을 띄운 후, 각 테스트 케이스마다 상원이의 생일 파티 초대장을 받는 친구의 수를 출력한다.

*상원이의 친구가 없을 수도 있다는 점에 유의해야 한다. 그리고 상원이는 초대장을 받는 사람에 속하지 않는다.




#### 풀이1

```python
'''
2
6 5
2 3
3 4
4 5
5 6
2 5
6 5
1 2
1 3
3 4
2 3
4 5
'''
def dfs(v, cnt):
    global ans
    if cnt == 2:
        return
    else:
        for w in range(N+1):
            if friends[v][w] and cnt < 2:
                invited[w] = 1
                dfs(w, cnt+1)

for tc in range(1, int(input())+1):
    N, M = map(int, input().split())
    friends = [[0]*(N+1) for _ in range(N+1)]
    for _ in range(M):
        a,b = map(int,input().split())
        friends[a][b] = 1
        friends[b][a] = 1
    # for row in friends:
    #     print(row)
    # print()

    invited = [0]*(N+1)

    dfs(1, 0)
    if sum(invited) == 0:
        ans = 0
    else:
        ans = sum(invited)-1

    print("#{} {}".format(tc, ans))
```

- 내 풀이

### 풀이2

```python
def bfs(v):  # v :시작점
    # 큐생성
    q = []
    # 시작점 넣기
    q.append(v)
    visited[v] = 1
    cnt = 0
    level = 0
    while q:
        s = len(q)  # 현재큐의 길이
        for j in range(s):  # 현재 레벨안에서 반복
            t = q.pop(0)  # 큐에서 하나 가져옴
            for i in adj[t]:
                if visited[i] == 0:
                    q.append(i)
                    visited[i] = 1
                    cnt += 1
        level += 1
        if level == 2: break
    return cnt

T = int(input())
for tc in range(1, T + 1):
    # 그래프 표현 -> 인접리스트
    N, M = map(int, input().split())
    adj = {i: [] for i in range(N + 1)}  # 인접리스트 초기화
    for i in range(M):  # 간선의 갯수만큼 반복
        a, b = map(int, input().split())
        adj[a].append(b)
    # print(adj)
    visited = [0] * (N + 1)
    print("#{} {}".format(tc, bfs(1)))
```

- 교수님께 배운 풀이, 혼자 연습도 해봤습니다.