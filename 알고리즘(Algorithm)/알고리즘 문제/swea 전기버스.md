# swea

# 전기버스

### 일자 20200829~20200830

#### 문제

A도시는 전기버스를 운행하려고 한다. 전기버스는 한번 충전으로 이동할 수 있는 정류장 수가 정해져 있어서, 중간에 충전기가 설치된 정류장을 만들기로 했다.

버스는 0번에서 출발해 종점인 N번 정류장까지 이동하고, 한번 충전으로 최대한 이동할 수 있는 정류장 수 K가 정해져 있다.

충전기가 설치된 M개의 정류장 번호가 주어질 때, 최소한 몇 번의 충전을 해야 종점에 도착할 수 있는지 출력하는 프로그램을 만드시오.

만약 충전기 설치가 잘못되어 종점에 도착할 수 없는 경우는 0을 출력한다. 출발지에는 항상 충전기가 설치되어 있지만 충전횟수에는 포함하지 않는다. 

**[입력]**


첫 줄에 노선 수 T가 주어진다. ( 1 ≤ T ≤ 50 )


각 노선별로 K, N, M이 주어지고, 다음줄에 M개의 정류장 번호가 주어진다. ( 1 ≤ K, N, M ≤ 100 )


**[출력]**


\#과 노선번호, 빈칸에 이어 최소 충전횟수 또는 0을 출력한다.

 

| 정류장 | 1    | 2    | 3    | 4    | 5    |
| ------ | ---- | ---- | ---- | ---- | ---- |
| 충전지 | 2    | 3    | 1    | 1    |      |



1번에서 장착한 충전지 용량이 2이므로, 3번 정류장까지 운행할 수 있다. 그러나 2번에서 미리 교체하면 종점까지 갈 수 있다.

마지막 정류장에는 배터리가 없다.


**[입력]**

첫 줄에 테스트케이스의 수 T가 주어진다. 1<=T<=50

다음 줄부터 테스트 케이스의 별로 한 줄에 정류장 수 N, N-1개의 정류장 별 배터리 용량 Mi가 주어진다. 3<=N<=100, 0 ＜ Mi ＜ N


**[출력]**

각 줄마다 "#T" (T는 테스트 케이스 번호)를 출력한 뒤, 답을 출력한다



#### 풀이

```python
T = int(input())
for tc in range(1,T+1):
    K, N, M = map(int,input().split())
    arr = list(map(int,input().split()))
    stations = [0]*(N+1)
    for chr in arr:
        stations[chr] = 1
    # print(stations)
    start_idx = 0
    cnt = 0
    bool = True
    while start_idx < N-K:
        if bool == False:
            break
        if stations[start_idx+K] == 1:
            cnt += 1
            start_idx = start_idx+K
        else:
            for i in range(1,K+1):
                if i == K: bool = False; break
                elif stations[(start_idx+K)-i] == 1:
                    start_idx = (start_idx+K)-i
                    cnt+=1
                    break
    if bool == True:
        print("#{} {}".format(tc, cnt))
    else: print("#{} 0".format(tc))
```

- SWEA 역량테스트 IM대비를 위해 시간이지나 까먹을 수 있는 부분들을  다시 한 번 풀며 복습해봤다.(0829기준)
- 매우 기본적인 문제지만 html/css와 django 학습 후 다시 알고리즘을 보니 매우 새로운 기분이 들었다.

