# swea

# 요리사

### 일자 20201204

### 문제

[본문 링크 참조](https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AWIeUtVakTMDFAVH&categoryId=AWIeUtVakTMDFAVH&categoryType=CODE)

#### 풀이1

```python
import copy

def cook(cnt, k, ing1, ing2):
    global ans
    if cnt == kinds:
        one, two = 0, 0
        for i in range(kinds-1):
            for j in range(i+1,kinds):
                one += (arr[ing1[i]][ing1[j]] + arr[ing1[j]][ing1[i]])
                two += (arr[ing2[i]][ing2[j]] + arr[ing2[j]][ing2[i]])
        ans = min(ans,abs(one-two))
        return
    for i in range(k, N):
        for j in range(k, N):
            if i!=j and not i in ing1 and not i in ing2 and not j in ing1 and not j in ing2:
                ing1.append(i); ing2.append(j)
                cook(cnt+1,i+1,copy.deepcopy(ing1),copy.deepcopy(ing2))
                ing1.pop(); ing2.pop()

for tc in range(1, int(input())+1):
    N = int(input())
    arr = [list(map(int, input().split())) for _ in range(N)]

    ans = 0xfffff

    kinds = N//2
    cook(0, 0, [], [])
    print("#{} {}".format(tc, ans))
```

#### 풀이2

```python
def cook(cnt, scale):
    global ans
    if cnt == kinds:
        dish1, dish2 = [], []
        for i in range(N):
            if visit[i]:
                dish1.append(i)
            else:
                dish2.append(i)
        one, two = 0, 0
        for i in range(kinds-1):
            for j in range(i+1,kinds):
                one += (arr[dish1[i]][dish1[j]] + arr[dish1[j]][dish1[i]])
                two += (arr[dish2[i]][dish2[j]] + arr[dish2[j]][dish2[i]])
        ans = min(ans,abs(one-two))
    for i in range(scale, N):
        visit[i] = 1
        cook(cnt+1, i+1)
        visit[i] = 0

for tc in range(1, int(input())+1):
    N = int(input())
    arr = [list(map(int, input().split())) for _ in range(N)]

    ans = 0xfffff

    kinds = N//2
    visit = [0]*N
    cook(0, 0)

    print("#%d %d"%(tc, ans))
```

- 두 개의 다른 방법으로 풀어 보았다.