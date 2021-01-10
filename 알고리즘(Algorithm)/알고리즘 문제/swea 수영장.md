# swea

# 수영장

### 일자 20201020

### 문제

[본문참조 링크](https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AV5PpFQaAQMDFAUq&categoryId=AV5PpFQaAQMDFAUq&categoryType=CODE)

### 풀이

```python
def dfs(mon, acc):
    global min_cost
    if mon == 13:
        if min_cost > acc:
            min_cost = acc
        return
    elif mon < 13:
        dfs(mon+1, acc + plan[mon]*day)
        dfs(mon+1, acc + month)
        dfs(mon+3, acc+thmonth)


for tc in range(1,int(input())+1):
    day, month, thmonth, year = map(int,input().split())
    plan = [0]+list(map(int, input().split()))
    min_cost = year
    dfs(1, 0)
    print("#%d" % tc, min_cost)
```

- 코드만 보면 간단한 문제이지만, 이 문제를 깊이우선 탐색(dfs)를 이용해 모든 경우의 수를 비교하며 답을 찾아내야 한다는 발상을 하지 못하면 풀지 못하는 문제이다.
- 당시에 이런 유형의 문제를 처음 접해봐, 처음 풀이는 DFS를 발상하지 못하고 엄한 방법으로 수리적으로 나올 수 있는 모든 경우의 수를 세세히 코드로 짰던 기억이 난다.

#### 풀이2(20201203에 다시 풀어봄.)

````python
import sys; sys.stdin = open('수영장.txt', 'r')

def go(months, acc):
    global result
    if acc >= result:
        return
    if months >= 12: # 1년 이 다 지난다면
        if acc < result:
            result = acc # 최소비용을 정답으로 최신화
        return
    go(months+1,acc+scheme[months]*day) # 일일권을 사용하는 경우
    go(months+1,acc+month) # 한달권 사용
    go(months+3, acc+triple) # 3달궈 사용
    go(months+12, acc+year) # 1년권 사용
    # 위와 같이 모든 경우의 수를 헤아려 준다.

for tc in range(1,int(input())+1):
    day, month, triple, year = map(int,input().split()) # 이용요금 정보 받기
    scheme = list(map(int, input().split())) # 일년 수영장 이용계획 정보 받기
    # print(scheme)

    result = 0xffffff
    go(0, 0) # dfs를 이용해 모든 경우의 수를 파악해 최소비용을 알아낼것이다.
    print("#%d" %tc, result)
````

- 이때는 망설임 없이 바로 풀 수 있었다.