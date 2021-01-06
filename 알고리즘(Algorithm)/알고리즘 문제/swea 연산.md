# swea

# 연산

### 일자 20201107

### 문제

자연수 N에 몇 번의 연산을 통해 다른 자연수 M을 만들려고 한다.

사용할 수 있는 연산이 +1, -1, *2, -10 네 가지라고 할 때 최소 몇 번의 연산을 거쳐야 하는지 알아내는 프로그램을 만드시오.

단, 연산의 중간 결과도 항상 백만 이하의 자연수여야 한다.

예를 들어 N=2, M=7인 경우, (2+1) *2 +1 = 7이므로 최소 3번의 연산이 필요한다.


**[입력]**

첫 줄에 테스트 케이스의 개수가 주어지고, 다음 줄부터 테스트 케이스 별로 첫 줄에 N과 M이 주어진다. 1<=N, M<=1,000,000, N!=M

**[출력]**

각 줄마다 "#T" (T는 테스트 케이스 번호)를 출력한 뒤, 답을 출력한다.

#### 풀이

```python
'''
3
2 7
3 15
36 1007
'''
def calc(n,i):
    if i == 0:
        return n+1
    elif i == 1:
        return n-1
    elif i == 2:
        return n*2
    elif i == 3:
        return n-10

def bfs():
    Q = [0]*1000000
    rear, front = -1, -1
    rear += 1
    Q[rear] = (N,0)

    while rear != front:
        front += 1
        num, cnt = Q[front]
        if num == M:
            return cnt
        for i in range(4):
            result = calc(num, i)
            if 0 < result <= 1000000 and visit[result] == -1:
                visit[result] = visit[num]+1
                rear += 1
                Q[rear] = (result,  cnt+1)
    return visit[M]

from collections import deque

def bfs2():
    Q = deque()
    Q.append(N)
    ans = 0

    while Q:
        size = len(Q)
        for i in range(size):
            num = Q.popleft()
            if num == M:
                return ans
            for j in (num+1, num-1, num*2, num-10):
                if 0 < j <= 1000000 and visit[j] == -1:
                    visit[j] = 1
                    Q.append(j)
        ans += 1

for tc in range(1,int(input())+1):
    N, M = map(int, input().split())

    visit = [-1]*1000001
    print("#%d" % tc, bfs2())
```
