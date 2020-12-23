# swea

# 화물 도크

### 일자 20201030

### 문제

24시간 운영되는 물류센터에는 화물을 싣고 내리는 도크가 설치되어 있다.

0시부터 다음날 0시 이전까지 A도크의 사용신청을 확인해 최대한 많은 화물차가 화물을 싣고 내릴 수 있도록 하면, 최대 몇 대의 화물차가 이용할 수 있는지 알아내 출력하는 프로그램을 만드시오.

신청서에는 작업 시작 시간과 완료 시간이 매시 정각을 기준으로 표시되어 있고, 앞 작업의 종료와 동시에 다음 작업을 시작할 수 있다.

예를 들어 앞 작업의 종료 시간이 5시면 다음 작업의 시작 시간은 5시부터 가능하다.


**[입력]**

첫 줄에 테스트케이스의 수 T가 주어진다. 1<=T<=50

다음 줄부터 테스트 케이스의 별로 첫 줄에 신청서 N이 주어지고, 다음 줄부터 N개의 줄에 걸쳐 화물차의 작업 시작 시간 s와 종료 시간 e가 주어진다.

1<=N<=100, 0<=s<24, 0 ＜ e ＜= 24 


**[출력]**

각 줄마다 "#T" (T는 테스트 케이스 번호)를 출력한 뒤, 답을 출력한다.

#### 풀이1

```python
for tc in range(1, int(input())+1):
    N = int(input())
    s_e_info = [list(map(int, input().split())) for _ in range(N)]
    s_e_info.sort(key=lambda x:x[1])
    # print(s_e_info)
    temp_truck = s_e_info[0]
    ans = 1
    for i in range(1,N):
        if temp_truck[1] <= s_e_info[i][0]:
            ans+=1
            temp_truck = s_e_info[i]
        else: continue
    print("#%d" % tc, ans)
```

- 이 문제 또한 `컨테이너 운반` 문제와 마찬가지로 sort 함수를 사용해주면 훨씬 풀기 쉬워진다.

#### 풀이2

```python
def doking(k, cnt):
    global max_trucks
    if k == len(s_e_info):
        if max_trucks < cnt:
            max_trucks = cnt
        return
    info = s_e_info[k]
    s, e = info[0], info[1]
    if not hours[e-1] and not hours[s] and not hours[(s+e-1)//2]:
        for i in range(s,e):
            hours[i] = 1
        doking(k+1,cnt+1)
        for i in range(s,e):
            hours[i] = 0
    doking(k+1,cnt)

T = int(input())
for tc in range(1,T+1):
    N = int(input())
    s_e_info = [list(map(int, input().split())) for _ in range(N)]
    # print(s_e_info)
    hours = [0]*25
    max_trucks = 0
    doking(0, 0)
    print("#{} {}".format(tc, max_trucks))
```

- sort 함수를 사용해 주지 않고 재귀함수를 이용해 풀어보기도 했다.
- 너무 파이썬 라이브러리에 의존하면 다른 언어를 학습할 때 좋지 않을 것 같아, 라이브러리를 사용하지 않는 법도 함께 훈련하려고 노력중이다.