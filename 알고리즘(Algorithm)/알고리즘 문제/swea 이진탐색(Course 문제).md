# swea

# 이진탐색(Course 문제)

### 일자 20200910

### 문제

1부터 N까지의 자연수를 이진 탐색 트리에 저장하려고 한다.

이진 탐색 트리는 어떤 경우에도 저장된 값이 왼쪽 서브트리의 루트 <현재 노드 <오른쪽 서브 트리의 루트인 규칙을 만족한다.

추가나 삭제가 없는 경우에는, 완전 이진 트리가 되도록 만들면 효율적인 이진 탐색 트리를 만들수 있다.

완전 이진 트리의 노드 번호는 루트를 1번으로 하고 아래로 내려가면서 왼쪽에서 오른쪽 순으로 증가한다.

N이 주어졌을 때 완전 이진 트리로 만든 이진 탐색 트리의 루트에 저장된 값과, N/2번 노드(N이 홀수인 경우 소수점 버림)에 저장된 값을 출력하는 프로그램을 만드시오.

**[입력]**

첫 줄에 테스트케이스의 수 T가 주어진다. 1<=T<=50

다음 줄부터 테스트 케이스의 별로 N이 주어진다. 1<=N<=1000

**[출력]**

각 줄마다 "#T" (T는 테스트 케이스 번호)를 출력한 뒤, 답을 출력한다.

#### 풀이1

```python
'''
3
6
8
15
'''
#쉽게생각하자!ㅡㅡ#
def inorder(n,):
    global order
    if n <= N:
        inorder(2*n)
        tree[n] = order
        order += 1
        inorder(2*n+1)

T = int(input())
for tc in range(1,T+1):
    N = int(input())
    # E = N-1
    info = [i for i in range(N+1)]
    # print(info)
    tree = [0]*(N+1)
    order = 1
    inorder(1)
    print("#{} {} {}".format(tc, tree[1], tree[N//2]))
```

#### 풀이2

```python
for tc in range(1,int(input())+1):
    N = int(input())
    T = [0]*(N+1)
    cnt = 1
    def inorder(v):
        global cnt
        if v > N: return
        inorder(v*2)
        T[v] = cnt
        cnt += 1
        inorder(v*2+1)
    inorder(1)
    print(T[1], T[N//2])
```

- 두 가지 방식으로 SWEA coures intermediate level의 이진탐색 문제를 풀어보았다.
- 한개의 풀이는 내가 풀어본 방식이고 나머지 하나는 교수님의 풀이법이다.
- 교수님의 풀이는 학습 후 혼자 코딩을 짜보는 시간을 가졌다.