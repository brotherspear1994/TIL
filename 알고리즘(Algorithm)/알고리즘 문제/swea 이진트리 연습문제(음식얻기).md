# swea

# 이진트리 연습문제(음식얻기)

### 일자 20201019



#### 풀이1

```python
'''
2
8
0 0 0 0 0 0 0 0
0 1 1 1 0 0 0 0
0 1 10 1 0 0 0 0
0 1 1 1 0 0 0 0
0 0 0 0 1 1 1 0
0 0 0 0 1 10 1 0
0 0 0 0 1 1 1 0
0 0 0 0 0 0 0 0
8
0 0 0 0 0 0 0 0
0 1 1 1 0 0 0 0
0 1 20 1 0 0 0 0
0 1 1 1 0 0 0 0
0 0 0 0 1 1 1 0
0 0 0 0 1 30 1 0
0 0 0 0 1 1 1 0
0 0 0 0 0 0 0 0
'''

def subtree_plus(idx, pick_stack, used_stack):
    distance = 0
    if pick_stack:
        for a in range(len(house_stack)):
            min_dis = 1000
            idx_cnt = 0
            c = -1
            for b in pick_stack:
                idx_cnt += 1
                dis_sub = abs(store_stack[b][0]-house_stack[a][0])+abs(store_stack[b][1]-house_stack[a][1])
                if min_dis > dis_sub: min_dis = dis_sub; c = b
                if idx_cnt == len(pick_stack):
                    distance += min_dis
                    if c != -1: used_stack.append(c)

    if idx == len(store_value_stack):
        if used_stack:
            for z in set(used_stack):
                distance += store_value_stack[z]
            ans_stack.append(distance)
            return
        else:
            return
    subtree_plus(idx+1, pick_stack, used_stack)
    pick_stack.append(idx)
    subtree_plus(idx+1, pick_stack, used_stack)
    pick_stack.pop()



T = int(input())
for tc in range(1,T+1):
    N = int(input())
    arr = [list(map(int, input().split())) for _ in range(N)]
    # for a in arr:
    #     print(*a)
    # print()
    house_stack = []
    store_stack = []
    store_value_stack = []
    for i in range(N):
        for j in range(N):
            if arr[i][j] >= 2: store_stack.append([i,j]); store_value_stack.append(arr[i][j])
            elif arr[i][j] == 1: house_stack.append([i,j])
    # print(house_stack)
    # print(store_stack)
    # print(store_value_stack)
    # print()
    ans_stack = []
    subtree_plus(0, [], [])
    # print(ans_stack)
    ans = min(ans_stack)
    print('#{} {}'.format(tc, ans))
```



#### 풀이2

```python
def solve(k):
    global ans
    if k == len(food):
        tsum = 0
        for h in range(len(home)):
            tmin = 1e9
            for f in range(len(subset)):
                if subset[f]:
                    tmin = min(tmin, dist[f][h])
            tsum += tmin
        for f in range(len(subset)):
            if subset[f]:
                tsum += food[f][2]
        if ans > tsum:
            ans=tsum
    else:
        subset[k] = 1
        solve(k+1)
        subset[k] = 0
        solve(k+1)


for tc in range(1, int(input())+1):
    N = int(input())
    mat = [list(map(int, input().split())) for _ in range(N)]
    home, food = [], []
    for i in range(N):
        for j in range(N):
            if mat[i][j] == 1:
                home.append((i,j))
            elif mat[i][j] > 1:
                food.append((i,j,mat[i][j]))

    dist = [[0]*len(home) for i in range(len(food))]

    for i in range(len(food)):
        for j in range(len(home)):
            dist[i][j] = abs(food[i][0]-home[j][0]) + abs(food[i][1]-home[j][1])
    # print(dist)
    ans = 1e9
    subset = [0]*len(food)
    solve(0)
    print(food)
    print(home)
    print(dist)
    print("#%d" % tc, ans)
```



#### 풀이4

```python
def subset(k):
    global ans
    if k == len(subset_check):
        sub_sum = 0
        for h in range(len(home)):
            subt = 1e9
            for f in range(len(subset_check)):
                if subset_check[f]:
                    subt = min(subt, dist[f][h])
            sub_sum += subt
        for f in range(len(subset_check)):
            if subset_check[f]:
                sub_sum += food[f][2]
        if ans > sub_sum: ans = sub_sum
    else:
        subset_check[k] = 1
        subset(k+1)
        subset_check[k] = 0
        subset(k+1)


for tc in range(1, int(input())+1):
    N = int(input())
    mat = [list(map(int, input().split())) for _ in range(N)]
    home, food = [], []
    for i in range(N):
        for j in range(N):
            if mat[i][j] == 1:
                home.append((i,j))
            elif mat[i][j] > 1:
                food.append((i,j,mat[i][j]))
    dist = [[0]*len(home) for _ in range(len(food))]

    for i in range(len(food)):
        for j in range(len(home)):
            dist[i][j] = abs(food[i][0]-home[j][0])+abs(food[i][1]-home[j][1])
    # for d in dist:
    #     print(*d)
    # print()
    ans = 1e9
    subset_check = [0]*len(food)
    subset(0)
    print("#%d" % tc, ans)
```

