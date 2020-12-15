# 힙(Heap)

[TOC]

### heappush(삽입)

```python
def heappush(value):
    global heapcount    #마지막 위치
    heapcount += 1      #지금 들어온 원소가 저장될 위치
    heap[heapcount] = value
    cur = heapcount  # 방금 들어온 값 위치
    parent = cur // 2  # cur의 부모
    # 루트 아니고 부모노드값 > 자식노드 값 => 바꾸기
    while parent and heap[parent] > heap[cur]:
        heap[parent], heap[cur] = heap[cur], heap[parent]
        cur = parent
        parent = cur // 2
        
        
temp = [7, 2, 5, 3, 4, 6]
N = len(temp)
heapcount = 0   #마지막으로 원소가 들어간 곳
heap = [0] * (N + 1)    #heap을 위한 배열 생성
for i in range(N):
    heappush(temp[i])
print(heap)
for i in range(N):
    print(heappop(), end=" ")
print()
```



### heappop(삭제)

```python
def heappop():
    global heapcount
    retValue = heap[1]  # 루트의 값을 리턴하기위해 준비
    heap[1] = heap[heapcount]  # 루트값 <- 마지막 원소로
    heap[heapcount] = 0  # 마지막원소 지우기
    heapcount -= 1  # 힙카운트 줄이기

    parent = 1      #root부터 시작
    child = parent * 2  # 왼쪽 자식

    if child + 1 <= heapcount:  # 오른쪽 자식 존재
        if heap[child] > heap[child + 1]:
            # 오른쪽 자식 < 왼쪽자식 => 우리는 둘중에 작은 값 찾아야함
            child = child + 1  # 부모랑 비교할 자식을 오른쪽으로
    # 자식 노드가 존재하고, 부모 노드 > 자식노드 => 바꾸기
    while child <= heapcount and heap[parent] > heap[child]:
        heap[parent], heap[child] = heap[child], heap[parent]
        parent = child  # 부모 <- 자식으로 갱신
        child = parent * 2  # 현 부모의 자식을 찾기
        if child + 1 <= heapcount:  # 오른쪽 자식있으면 둘중 작은 값을 찾음
            if heap[child] > heap[child+1]:
                child = child + 1
    return retValue


temp = [7, 2, 5, 3, 4, 6]
N = len(temp)
heapcount = 0   #마지막으로 원소가 들어간 곳
heap = [0] * (N + 1)    #heap을 위한 배열 생성
for i in range(N):
    heappush(temp[i])
print(heap)
for i in range(N):
    print(heappop(), end=" ")
print()
```



### heap 라이브러리 활용

```python
# 라이브러리

# 최소힙만 지원(heapq)
import heapq

heap1 = [7, 2, 5, 3, 4, 6]
print(heap1)
heapq.heapify(heap1)
print(heap1)
heapq.heappush(heap1, 5)
print(heap1)
while heap1:
    print(heapq.heappop(heap1), end=' ')
print()
# ------------------------------

# 최대힙
heap1 = [7, 2, 5, 3, 4, 6]
heap2 = []
# for i in range(len(temp)):
#     heapq.heappush(heap2, (-temp[i], temp[i]))  # 우선순위, 데이터
# heapq.heappush(heap2, (-1, 1))
# print(heap2)
# while heap2:
#     print(heapq.heappop(heap2)[1], end=" ")

for i in range(len(heap1)):
    heapq.heappush(heap2, (-heap1[i],heap1[i]))
print(heap2)
while heap2:
    print(heapq.heappop(heap2)[1], end=" ")
print()
```



### heap 연습(혼자 해보기)

```python
def heappop():
    global heapcount
    retValue = heap[1]
    heap[1], heap[heapcount] = heap[heapcount], heap[1]
    heap[heapcount] = 0
    heapcount -= 1
    parent = 1
    child = 1*2
    while child <= heapcount:
        if child + 1 <= heapcount:
            if heap[child] > heap[child + 1]:
                child = child + 1
        if heap[parent] > heap[child]:
            heap[parent], heap[child] = heap[child], heap[parent]
        parent = child
        child = parent*2
    return retValue

def heappush_second(value):
    global heapcount
    heapcount += 1
    heap[heapcount] = value
    child = heapcount
    parent = heapcount//2
    while parent:
        if heap[parent] > heap[child]:
            heap[parent], heap[child] = heap[child], heap[parent]
        child = parent
        parent = child//2


temp = [7, 2, 5, 3, 4, 6]
N = len(temp)
heapcount = 0
heap = [0] * (N+1)
for i in range(N):
    heappush_second(temp[i])
# print(heap)
for i in range(N):
    print(heappop(), end=" ")
print()
```

- heap을 학습한지 오래돼 heap 알고리즘을 다시 복습했다.

- MST Prim이나 Dijkstra 알고리즘 문제를 해결할때 heap을 활용하면 자동으로 가중치를 오름차순으로 정렬해주기 때문에 유용하여, heap을 활용해 문제들을 풀기위해 복습했다.

  

