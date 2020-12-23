# swea

# 컨테이너 운반

### 일자 20201030

### 문제

화물이 실려 있는 N개의 컨테이너를 M대의 트럭으로 A도시에서 B도시로 운반하려고 한다.

트럭당 한 개의 컨테이너를 운반 할 수 있고, 트럭의 적재용량을 초과하는 컨테이너는 운반할 수 없다.

컨테이너마다 실린 화물의 무게와 트럭마다의 적재용량이 주어지고, A도시에서 B도시로 최대 M대의 트럭이 편도로 한번 만 운행한다고 한다.

이때 이동한 화물의 총 중량이 최대가 되도록 컨테이너를 옮겼다면, 옮겨진 화물의 전체 무게가 얼마인지 출력하는 프로그램을 만드시오.

화물을 싣지 못한 트럭이 있을 수도 있고, 남는 화물이 있을 수도 있다. 컨테이너를 한 개도 옮길 수 없는 경우 0을 출력한다.


**[입력]**

첫 줄에 테스트케이스의 수 T가 주어진다. 1<=T<=50

다음 줄부터 테스트 케이스의 별로 첫 줄에 컨테이너 수 N과 트럭 수 M이 주어지고, 다음 줄에 N개의 화물이 무게wi, 그 다음 줄에 M개 트럭의 적재용량 ti가 주어진다.

1<=N, M<=100, 1<=wi, ti<=50
 
**[출력]**

각 줄마다 "#T" (T는 테스트 케이스 번호)를 출력한 뒤, 답을 출력한다.

#### 풀이

```python
'''
3
3 2
1 5 3
8 3
5 10
2 12 13 11 18
17 4 7 20 3 9 7 9 20 5
10 12
10 13 14 6 19 11 5 20 11 14
5 18 17 8 9 17 18 4 1 16 15 13
'''
for tc in range(1, int(input())+1):
    N, M = map(int, input().split())
    W = list(map(int,input().split()))
    T = list(map(int,input().split()))
    W.sort(reverse=True)
    T.sort(reverse=True)

    i, j, ans = 0, 0, 0

    while i < N and j < M:
        if W[i] <= T[j]:
            ans += W[i]
            i, j = i+1, j+1
        else:
            i += 1
    print("#%d" % tc, ans)
```

- python 라이브러리의 sort reverse 기능을 활용해 주는게 포인트!



#### 풀이2(백트랙킹 실패 코드)

```python
def load(weight, trucks, weights):
    global max_weight
    for i in range(len(trucks)):
        if loaded[i]: continue
        for j in range(len(weight)):
            if trucks[i] >= weight[j] and not loaded[i] and not weight[j] in weights:
                weights.append(weight[j])
                loaded[i] = 1
                load(weight, trucks, weights)
                weights.pop()
                loaded[i] = 0
            else: continue
    if sum(weights) >= max_weight: max_weight = sum(weights)


for tc in range(1,int(input())+1):
    N, M = map(int,input().split())
    w = list(map(int,input().split()))
    t = list(map(int,input().split()))
    # print(N, M)
    # print(w)
    # print(t)
    max_weight = 0
    loaded = [0]*len(t)
    weights = []
    load(w, t, weights)
    print("#{} {}".format(tc, max_weight))
```

- 맨처음 시도했던 풀이지만, 백트랙킹을 제대로 해주지 못해 런타임 에러가 발생했다.
- 때문에 아래와 같이 코드를 전부 갈아 엎었다.



#### 풀이3(시간단축 성공 코드)

```python
def load(k, loaded):
    global w; global max_weight
    temp = t[:]
    if k == len(t):
        return
    while k < len(t):
        load_loc = 0
        for i in range(len(w)):
            if temp[k] >= w[i] and w[i] >= loaded[k]:
                loaded[k] = w[i]
                load_loc = i
        w[load_loc] = 0
        k += 1
    max_weight = sum(loaded)


for tc in range(1,int(input())+1):
    N, M = map(int,input().split())
    w = list(map(int,input().split()))
    t = list(map(int,input().split()))
    loaded = [0]*len(t)
    max_weight = 0
    load(0, loaded)
    print("#%d" % tc, max_weight)
```