# Stack

[TOC]

### Stack 1

```python
# C style

stack = [0]*100 # 배열은 고정(씨언어에서는)
top = -1

def push(item):
    global top
    if top > 100 - 1:
        return
    else:
        top += 1
        stack[top] = item

def pop(): # isEmpty
    global top
    if top == -1:
        print("Stack is Empty!")
        return
    else:
        result = stack[top]
        top -= -1
        return result

stack = [0] * 100
top = -1

push(1)
push(2)
push(3)
print(pop())
print(pop())
print(pop())

```



### Stack 2

```python
stack = []

def push(item):
    stack.append(item)

def pop():
    if len(stack) == 0:
        print("Stack is empty!!")
        return
    else:
        return stack.pop()


push(1)
push(2)
push(3)

print(pop())
print(pop())
print(pop())
```



### Stack 3

```python
stack = []

stack.append(1)
stack.append(2)
stack.append(3)

if stack:
    print(stack.pop())
if stack:
    print(stack.pop())
if stack:
    print(stack.pop())
if stack:
    print(stack.pop())
```



### 스택 연습해보기

```python


# def check(arr):
#     for i in range(len(arr)):
#         if arr[i] == '(':
#             stack.append(arr[i])
#             print(stack)
#         elif arr[i] == ')':
#             if len(stack) == 0:
#                 return False
#             else:
#                 stack.pop()
#     if stack: return False
#     else: return True
#
# stack = []
# arr = "()()((()))"
# print(check(arr))

stack = []
def check(k):
    for i in range(len(k)):
        if k[i] == '(':
            stack.append(k[i])
        elif k[i] == ')':
            if len(stack) == 0:
                return False
            else:
                stack.pop()
    if len(stack):
        return False
    else:
        return True

arr = '((()))(('
print(check(arr))
```



### 응용문제(스택 1)

```python
import sys
sys.stdin = open('../0827/input.txt', 'r')

for _ in range(1,11):
    tc = int(input())
    arr = [list(map(int, input().split())) for _ in range(100)]
# for row in arr:
#     print(row)
    # 도착지점 인덱스 저장


    for n in range(100):
        if arr[99][n] == 2:
            x = n
            break
    # 도착지점부터 출발 시작
    y = 99
    while 1:
        # 오른쪽으로 가는경우, 오른쪽으로 이동후 올라감
        if x < 99 and arr[y][x+1]:
            while x < 99 and arr[y][x+1]:
                x += 1
            else:
                y -= 1
        elif x > 0 and arr[y][x-1]:
            while x > 0 and arr[y][x-1]:
                x -= 1
            else:
                y -= 1
        else:
            y -= 1

        if y == 0:
            break
    print(f'#{tc} {x}')

    # w = 0
    # top = 99
    # for i in range(len(arr[top])):
    #     if arr[99][i] == 2:
    #         w = i
    # # print(w)
    # # print(arr[99][58])
    # # 오른쪽 이동
    # while 1:
    #     if w < len(arr[top])-1 and arr[top][w + 1]:
    #         while w < len(arr[top])-1 and arr[top][w + 1]:
    #             w += 1
    #         else: top -= 1
    #     # 왼쪽 이동
    #     elif w > 0 and arr[top][w-1]:
    #         while w > 0 and arr[top][w-1]:
    #             w -= 1
    #         else: top -= 1
    #     else:
    #         top -= 1
    #
    #     if top == 0:
    #         print(w)
    #         break
```

- Stack을 세가지 방법으로 익혀보았다.
- 기본 개념학습 후 혼자 코드를 짜보는 시간을 가져본 후에는 SWEA의 Stack 응용문제를 풀어보는 시간을 가졌다.
- ![Stack Structure](https://miro.medium.com/max/1100/1*S2ujFRrOU_GJQOhhQD8LyA.png)
- 스택은 선입후출 자료구조.
- 마지막에 들어온 것이 먼저 나가는 LIFO(Last In First Out) 구조를 가진 자료 구조