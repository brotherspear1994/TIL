# swea

# 이진 힙

### 일자 20200910

### 문제

이진 최소힙은 다음과 같은 특징을 가진다.

  \- 항상 완전 이진 트리를 유지하기 위해 마지막 노드 뒤에 새 노드를 추가한다.

  \- 부모 노드의 값<자식 노드의 값을 유지한다. 새로 추가된 노드의 값이 조건에 맞지 않는 경우, 조건을 만족할 때까지 부모 노드와 값을 바꾼다.

  \- 노드 번호는 루트가 1번, 왼쪽에서 오른쪽으로, 더 이상 오른쪽이 없는 경우 다음 줄로 1씩 증가한다.

1000000이하인 N개의 서로 다른 자연수가 주어지면 입력 순서대로 이진 최소힙에 저장하고, 마지막 노드의 조상 노드에 저장된 정수의 합을 알아내는 프로그램을 작성하시오.

**[입력]**

첫 줄에 테스트케이스의 수 T가 주어진다. 1<=T<=50
다음 줄부터 테스트 케이스의 별로 N이 주어지고, 다음 줄에 1000000이하인 서로 다른 N개의 자연수가 주어진다. 5<=N<=500

**[출력]**

각 줄마다 "#T" (T는 테스트 케이스 번호)를 출력한 뒤, 답을 출력한다.

#### 풀이1

```python
def heappush(value):
    global heapcount
    heapcount += 1
    c = heapcount
    p = heapcount//2
    Tree[c] = value
    if p > 0 and Tree[p] > Tree[c]:
        while p > 0 and Tree[p] > Tree[c]:
            Tree[p], Tree[c] = Tree[c], Tree[p]
            c = p
            p = c//2

T = int(input())
for tc in range(1,T+1):
    N = int(input())
    Tree = [0]*(N+1)
    temp = list(map(int,input().split()))
    heapcount = 0
    for i in range(len(temp)):
        heappush(temp[i])
    lastnode= heapcount
    anc = lastnode // 2
    ans = 0
    while anc > 0:
        ans += Tree[anc]
        anc = anc // 2

    print("#{} {}".format(tc, ans))
```

#### 풀이2

```python
import heapq
T = int(input())
for tc in range(1,T+1):
    N = int(input())
    # print(N)
    info = list(map(int,input().split()))
    # print(info)
    heap = []
    for i in info:
        heapq.heappush(heap,i)
    heap = [0]+heap
    target = N//2
    ans = 0
    while target > 0:
        ans += heap[target]
        # print(target)
        target = target//2
    print(ans)
```

#### 풀이3

```python
def push(item):
    global hsize
    hsize += 1
    H[hsize] = item
    c=hsize; p=hsize//2
    while p and H[p] > H[c]:
        H[p], H[c] = H[c], H[p]
        c = p; p = c//2
for tc in range(1,int(input())+1):
    N = int(input())
    arr = list(map(int,input().split()))
    H = [0]* (N+1)
    hsize = 0
    for i in range(N):
        push(arr[i])
```



#### 풀이4

```python
for tc in range(1,int(input())+1):
    N = int(input())
    arr = list(map(int,input().split()))
    H = [0]* (N+1)
    hsize = 0
    for val in arr:
        hsize += 1
        H[hsize] = val

        c=hsize; p=hsize//2
        while p and H[p] > H[c]:
            H[p], H[c] = H[c], H[p]
            c = p; p = c//2

    ans = 0
    v = N//2
    while v:
        ans += H[v]
        v = v//2
    print(ans)
```



#### 풀이5

```python
######################### heapq 설명 ###################
from heapq import heapify

for tc in range(1,int(input())+1):
    N = int(input())
    arr = list(map(int,input().split()))

    heapify(arr)
    print(arr)
    # heapify는 0부터 노드를 때려넣음.
    
########################## heapq 활용 풀이#################
from heapq import heappush
for tc in range(1,int(input())+1):
    N = int(input())
    arr = list(map(int,input().split()))
    H = []
    for val in arr:
        heappush(H, val)
    H = [0]+H
    target = N//2
    ans = 0
    while target:
        ans += H[target]
        target //= 2
    print("#{} {}".format(tc, ans))
```

- 크게 다섯가지 방식으로 SWEA coures intermediate level의 이진힙 문제를 풀어보았다.
- 교수님 풀이를 보기전, 나 혼자 heappush 함수를 만들어 구현하는 법과 heapq 라이브러리를 활용하는 법, 두가지 방식을 사용해 풀어보았다.
- 이후 교수님이 세가지 풀이를 더 알려주셨다.
- 알려준 풀이법이 많아 추가적으로 더 학습하고 혼자 코딩을 가져보는데 다소 시간이 걸렸다. 다양한 풀이법을 익히는건 좋지만 힘든것 같다;;