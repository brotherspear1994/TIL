# Queue

[TOC]

` Queue의 개념은 BFS, DFS와 다소 혼돈하기 쉬워 정확한 개념과 차이점을 함께 남겨본다.`



- Queue algorithm

  ## Featured snippet from the Tutorialspoint 

  **Queue** is an abstract data structure, somewhat similar to Stacks. Unlike stacks, a **queue** is open at both its ends. One end is always used to insert data (enqueue) and the other is used to remove data (dequeue). **Queue** follows First-In-First-Out methodology, i.e., the data item stored first will be accessed first.



- 위에서 살펴본 바와 같이, 큐는 스택과 혼돈하기 쉬우나 데이터가 들어가는 장소와 나오는 장소를 한 곳으로 정하고, 먼저 들어가는 데이터는 나오는 장소에 먼저 도달하며(큐가 다 채워질 때)먼저 나오는 선입선출의 개념을 가진다.
- 아래에서는 rear와 front를 이용해 단순 리스트 모양의 Queue와 원형 모양의 Queue를 구현해 보는 시간을 가져보았다. 

### Queue 기본 

```python
# front, rear 이용
Q = [0] * 100
front, rear = -1, -1

def enQueue(item):
    global rear
    if rear == len(Q)-1:
        print("Queue Full")
    else:
        rear = rear + 1
        Q[rear] = item
def deQueue():
    global front
    if front == rear:
        print("Queue Empty")
    else:
        front += 1
        return Q[front]
def Qpeek():
    if front == rear:
        print("empty")
    else:
        return Q[front+1]
enQueue(1)
enQueue(2)
enQueue(3)
print(Qpeek())
print(deQueue())
print(deQueue())
print(deQueue())
print(deQueue())
```



### 원형 Queue

```python
SIZE = 4
Q = [0]*SIZE
front, rear = 0, 0

def enQueue(item):
    global rear
    if (rear+1)%SIZE == front: #full
        print("Queue Full")
    else:
        rear = (rear + 1) % SIZE
        Q[rear] = item
def deQueue():
    global front
    if front == rear:
        print("Queue Empty")
    else:
        front = (front+1)%SIZE
        return Q[front]
def Qpeek():
    if front == rear:
        print("empty")
    else:
        return Q[(front+1)%SIZE]
enQueue(1)
enQueue(2)
enQueue(3)
print(Qpeek())
print(deQueue())
print(deQueue())
print(deQueue())
print(deQueue())
enQueue(4)
enQueue(5)
print(Q)
```

- 먼저 집어 넣은 데이터가 먼저 나오는 FIFO (First In First Out)구조(선입선출)로 저장하는 형식을 말한다.
- 나중에 집어 넣은 데이터가 먼저 나오는 스택과는 반대되는 개념