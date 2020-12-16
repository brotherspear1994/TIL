# swea

# 공통조상

### 일자 20200911

### 문제

[본문 링크 참조](https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AV15PTkqAPYCFAYD&categoryId=AV15PTkqAPYCFAYD&categoryType=CODE)

#### 풀이

```python
def isancestor():
    for val in target1_s:
        if val in target2_s: return val

for tc in range(1,int(input())+1):
    V, E, target1, target2 = map(int,input().split())
    L = [0]*(V+1)
    R = [0]*(V+1)
    P = [0]*(V+1)
    info = list(map(int,input().split()))
    for i in range(0,E*2,2):
        if L[info[i]]:
            if L[info[i]] > info[i+1]:
                R[info[i]] = L[info[i]]
                L[info[i]] = info[i+1]
            else: R[info[i]] = info[i+1]
        else: L[info[i]] = info[i+1]
        P[info[i+1]] = info[i]
    # print(L)
    # print(R)
    # print(P)
    # print()
    target1_s = []
    target2_s = []
    target1_p, target2_p = P[target1], P[target2]
    while target1_p:
        target1_s.append(target1_p)
        target1_p = P[target1_p]
    while target2_p:
        target2_s.append(target2_p)
        target2_p = P[target2_p]
    ancestor = isancestor()
    count = 0
    def postorder(value):
        global count
        if value == 0: return
        count += 1
        postorder(L[value])
        postorder(R[value])
    postorder(ancestor)
    print("#{} {} {}".format(tc, ancestor, count))
```

- 이진트리의 특성을 활용해, 공통조상을 찾는 문제이다.
- 트리의 개념을 제대로 학습했다면 어렵지 않게 풀 수 있는 문제이다.