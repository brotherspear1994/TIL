# swea

# 최적경로

### 일자 20201103

#### 문제

삼성전자의 서비스 기사인 김대리는 회사에서 출발하여 냉장고 배달을 위해 N명의 고객을 방문하고 자신의 집에 돌아가려한다.

회사와 집의 위치, 그리고 각 고객의 위치는 이차원 정수 좌표 (x, y)로 주어지고 (0 ≤ x ≤ 100, 0 ≤ y ≤ 100)

두 위치 (x1, y1)와 (x2, y2) 사이의 거리는 |x1-x2| + |y1-y2|으로 계산된다.

여기서 |x|는 x의 절대값을 의미하며 |3| = |-3| = 3이다. 회사의 좌표, 집의 좌표, 고객들의 좌표는 모두 다르다.

회사에서 출발하여 N명의 고객을 모두 방문하고 집으로 돌아오는 경로 중 가장 짧은 것을 찾으려 한다.

회사와 집의 좌표가 주어지고, 2명에서 10명 사이의 고객 좌표가 주어질 때,

회사에서 출발해서 이들을 모두 방문하고 집에 돌아가는 경로 중 총 이동거리가 가장 짧은 경로를 찾는 프로그램을 작성하라.

여러분의 프로그램은 가장 짧은 경로의 이동거리만 밝히면 된다.

이 문제는 가장 짧은 경로를 ‘효율적으로’ 찾는 것이 목적이 아니다.

여러분은 모든 가능한 경로를 살펴서 해를 찾아도 좋다.

모든 경우를 체계적으로 따질 수 있으면 정답을 맞출 수 있다.

**[제약사항]**

고객의 수 N은 2≤N≤10 이다.

그리고 회사의 좌표, 집의 좌표를 포함한 모든 N+2개의 좌표는 서로 다른 위치에 있으며 좌표의 값은 0이상 100 이하의 정수로 이루어진다.

**[입력]**

가장 첫줄은 전체 테스트케이스의 수이다.

이후, 두 줄에 테스트 케이스 하나씩이 차례로 주어진다.

각 테스트 케이스의 첫째 줄에는 고객의 수 N이 주어진다. 둘째 줄에는 회사의 좌표,집의 좌표, N명의 고객의 좌표가 차례로 나열된다.

좌표는 (x,y)쌍으로 구성되는데 입력에서는 x와 y가 공백으로 구분되어 제공된다.

**[출력]**

총 10줄에 10개의 테스트 케이스 각각에 대한 답을 출력한다.

각 줄은 ‘#x’로 시작하고 공백을 하나 둔 다음 최단 경로의 이동거리를 기록한다. 여기서 x는 테스트 케이스의 번호다.



#### 풀이1

```python
def go(x, y, acc):
    global ans
    if acc >= ans:
        return
    if not 0 in visit:
        acc = acc+(abs(x-h_x)+abs(y-h_y))
        ans = min(acc, ans)
        return
    else:
        for i in range(0, 2*N, 2):
            if not visit[i] and not visit[i+1]:
                visit[i], visit[i+1] = 1, 1
                go(customs[i], customs[i+1], acc+(abs(x-customs[i])+abs(y-customs[i+1])))
                visit[i], visit[i+1] = 0, 0
 
for tc in range(1,int(input())+1):
    N = int(input())
    info = list(map(int,input().split()))
    # print(info)
    com_x, com_y = info[0], info[1]
    h_x, h_y = info[2], info[3]
    customs = info[4:]
    # print(customs)
 
    visit = [0]*(2*N)
    ans = 0xffffffffffff
    go(com_x, com_y, 0)
    print("#{} {}".format(tc, ans))
```



### 풀이2

```python
class Point:
    def __init__(self,x,y):
        self.x = x
        self.y = y
 
def perm(customer, idx, path, visited):
    global minV
    #모든 고객을 방문하면?
    if idx == N :
        #거리 계산
        # 회사 - 첫번째 방문 고객 -> 순열대로 방문
        #마지막 고객 - 집으로
        dist = 0
        dist += abs(company.x - path[0].x) + abs(company.y - path[0].y)
        for i in range(N-1):
            dist += abs(path[i].x - path[i+1].x) + abs(path[i].y - path[i+1].y)
        dist+= abs(path[N-1].x - home.x) + abs(path[N-1].y - home.y)
        if minV > dist:
            minV = dist
        return
    #아니면순열 계속 만들어 나감
    for i in range(N):
        if visited[i] == 0:
            path[idx] = customer[i]
            visited[i] = 1
            perm(customer,idx+1, path, visited)
            visited[i] = 0
 
T = int(input())
for tc in range(1,T+1):
    N = int(input())
    arr = list(map(int,input().split()))
    company = Point(arr[0],arr[1])
    home = Point(arr[2],arr[3])
    customer =[]
    for i in range(2,N+2):
        customer.append(Point(arr[2*i],arr[2*i+1]))
    visited = [0] * N
    minV = 100000
    path = [0] * N
    perm(customer,0,path,visited)
    print("#{} {}".format(tc,minV))
```

- 최적경로 문제를 두가지 방법으로 풀어보았다.
- 두번째 방법은 입력을 받을 때 Class를 활용해 각각의 요소를 클래스의 인스턴스로 만드는 방법을 활용했다.
- 객체지향 방식이라고 말할 수도 없지만, 차근차근 클래스를 활용한 객체지향형 코딩으로 알고리즘을  해결하는 법도 학습해야겠다.