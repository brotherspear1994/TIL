# swea

# 활주로 건설

### 일자 20201204

### 문제

[본문 링크 참조](https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AWIeW7FakkUDFAVH&categoryId=AWIeW7FakkUDFAVH&categoryType=CODE)

#### 풀이

```python
import sys; sys.stdin = open('활주로.txt', 'r')

import copy

for tc in range(1,int(input())+1):
    N, X = map(int,input().split())
    arr = [list(map(int,input().split())) for _ in range(N)]
    arr_sero = []
    for i in range(N):
        sero_sub = []
        for j in range(N):
            sero_sub.append(arr[j][i])
        arr_sero.append(sero_sub)

    ans = 0
    for i in range(N):
        # 가로 체크
        target = copy.deepcopy(arr[i][:])
        visit = [0]*N
        boolean = True
        for a in range(N-1):
            if not boolean: break
            if target[a]!=target[a+1]:
                # if abs(target[a]-target[a+1])>1: boolean=False; break
                if abs(target[a] - target[a + 1]) != 1: boolean = False; break
                if target[a] > target[a+1]:
                    airstrp = target[a+1:a+1+X]
                    if len(airstrp)!=X: boolean=False; break
                    if 1 in visit[a+1:a+1+X]: boolean=False;break
                    for s in range(X-1):
                        if airstrp[s] != airstrp[s+1]: boolean=False;break
                    visit[a+1:a+1+X] = map(lambda x:x+1, visit[a+1:a+1+X])
                else:
                    airstrp = target[a-X+1:a+1]
                    if len(airstrp) !=X: boolean=False; break
                    if 1 in visit[a-X+1:a+1]: boolean = False;break
                    for s in range(X-1):
                        if airstrp[s] != airstrp[s+1]: boolean=False;break
                    visit[a-X+1:a+1] = map(lambda x: x + 1, visit[a-X+1:a+1])
        if boolean:
            ans += 1

        # 세로 체크
        target = copy.deepcopy(arr_sero[i][:])
        visit = [0]*N
        boolean = True
        for a in range(N-1):
            if not boolean: break
            if target[a]!=target[a+1]:
                # if abs(target[a]-target[a+1])>1: boolean=False; break
                if abs(target[a] - target[a + 1]) != 1: boolean = False; break
                if target[a] > target[a+1]:
                    airstrp = target[a+1:a+1+X]
                    if len(airstrp)!=X: boolean=False; break
                    if 1 in visit[a+1:a+1+X]: boolean=False;break
                    for s in range(X-1):
                        if airstrp[s] != airstrp[s+1]: boolean=False;break
                    visit[a+1:a+1+X] = map(lambda x:x+1, visit[a+1:a+1+X])
                else:
                    airstrp = target[a-X+1:a+1]
                    if len(airstrp) !=X: boolean=False; break
                    if 1 in visit[a-X+1:a+1]: boolean = False;break
                    for s in range(X-1):
                        if airstrp[s] != airstrp[s+1]: boolean=False;break
                    visit[a-X+1:a+1] = map(lambda x: x + 1, visit[a-X+1:a+1])
        if boolean:
            ans += 1

    print("#%d %d"%(tc, ans))
```
