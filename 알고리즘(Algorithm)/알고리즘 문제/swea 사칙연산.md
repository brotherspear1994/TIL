# swea

# 사칙연산

### 일자 20200910

### 문제

[본문 링크 참조](https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AV141J8KAIcCFAYD&categoryId=AV141J8KAIcCFAYD&categoryType=CODE)

#### 풀이1

```python
def postorder(n):
    if type(tree[n][0]) == int:
        return
    if n <= N:
        postorder(tree[n][1])
        postorder(tree[n][2])
        if tree[n][0] == "+":
            tree[n][0]=tree[tree[n][1]][0]+tree[tree[n][2]][0]
        elif tree[n][0] == "-":
            tree[n][0]=tree[tree[n][1]][0]-tree[tree[n][2]][0]
        elif tree[n][0] == "*":
            tree[n][0]=tree[tree[n][1]][0]*tree[tree[n][2]][0]
        elif tree[n][0] == "/":
            tree[n][0]=float(tree[tree[n][1]][0]/tree[tree[n][2]][0])


for tc in range(1,11):
    N = int(input())
    tree = [[0]*3 for _ in range(N+1)]
    for _ in range(N):
        info = list(input().split())
        if len(info) == 4:
            row = int(info[0])
            tree[row][0] = info[1]
            tree[row][1] = int(info[2])
            tree[row][2] = int(info[3])
        if len(info) == 2:
            row = int(info[0])
            tree[row][0] = int(info[1])
    # for t in tree:
    #     print(*t)

    postorder(1)
    print("#{} {}".format(tc, int(tree[1][0])))
```

#### 풀이2

```python
for tc in range(1,11):
    N = int(input())
    T = [[]]
    for i in range(1,N+1):
        T.append(list(input().split()))
        if len(T[i]) == 4: # 연산자
            T[i][2] = int(T[i][2])
            T[i][3] = int(T[i][3])
        else:
            T[i][1] = int(T[i][1])
    def calc(v):
        if len(T[v]) == 2: # 피연산자
            return T[v][1]
        else:
            l = calc(T[v][2])
            r = calc(T[v][3])
            if T[v][1] == '+': return l+r
            elif T[v][1] == '-': return l-r
            elif T[v][1] == '*': return l*r
            else: return l/r
    print(calc(1))
```

#### 풀이3

```python
for tc in range(1,11):
    N = int(input())
    T=[[]]
    for _ in range(N):
        T.append(list(input().split()))
    for i in range(1,N+1):
        if len(T[i]) == 4:
            T[i][2] = int(T[i][2])
            T[i][3] = int(T[i][3])
        else: T[i][1] = int(T[i][1])
    def calc(idx):
        if len(T[idx]) == 2: return T[idx][1]
        else:
            l = calc(T[idx][2])
            r = calc(T[idx][3])
            if T[idx][1] == '+': return l+r
            if T[idx][1] == '-': return l-r
            if T[idx][1] == '*': return l*r
            else: return l/r
    print("#{} {}".format(tc, int(calc(1))))
```

- 크게 세 가지 방식으로 사칙연산 문제를 풀어보았다.
- 풀이1은 내가 처음에 풀었던 코드이고 이후 두개의 코드는 교수님이 수업시간 동안 알려준 코드이다.
- 둘다 모두 학습 후 혼자 짜보는 시간을 가졌으며, 특히 풀이3은 내가 짠 코드보다 훨씬 깔끔하고 심플해서 몇번더 연습하는 시간을 가졌다.