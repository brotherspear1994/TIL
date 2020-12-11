# 부분집합(subset)

[TOC]

### 부분집합(재귀함수 1)

```python
def subset(n):
    if n == N:
        # 출력
        for i in range(N):
            if bit[i]:
                print(arr[i], end=" ")
        print()
        return
    # 선택, 비선택
    bit[n] = 0
    subset(n+1)
    bit[n] = 1
    subset(n+1)

arr = [1,2,3] #선택할 원소가 모인 배열
N = len(arr)
bit = [0] * N #원소 선택여부 저장
subset(0)
```



### 부분집합(비트마킹)

```python
arr = [1,2,3,4,5]
n = len(arr)

for i in range(1<<n):
    for j in range(5):
        if i & (1<<j):
            print(arr[j], end=' ')
    print()
```



### 부분집합(재귀함수 2)

```python
def subset(idx, stack):
    if idx == len(arr)-6:
        print(stack)
        return
    else:
        stack.append(arr[idx-4])
        subset(idx-1,stack)
        stack.pop()
        subset(idx-1,stack)
stack = []
subset(4, stack)

def subset(num,visit):
    if num==5:
        for i in visit:
            if i:
                print(i, end=' ')
        print()
        return
    visit[num] = num + 1
    subset(num+1, visit)
    visit[num] = 0
    subset(num+1, visit)


visit = [0]*5
subset(0, visit)
```

- 모든 부분집합을 출력하는 알고리즘을, 3가지 방식으로 표현해봤다.

- 첫번째 부분집합은 9월에 익혔고, 이후 시간이 지나 나머지 두개의 방식은 10월말에 익혔다.

- 세가지 방식 모두 수업시간 동안 개념을 정확히 학습한 후 직접 코드를 구현해 보는 시간을 가졌다.

- 이후 개인학습을 통해 복습하는 시간도 가졌다. 부분집합 알고리즘은 코드로 짤 줄은 알아도 몬가 100퍼센트 이해를 한 느낌이 아니어서, 한 알고리즘 당 최소 3~4번은 연습하며 이해하려고 노력한 것 같다.

  - 특히 비트마킹을 통해  부분집합을 출력하는 알고리즘을 구현하며, 어느정도 작은 깨닳음을 얻은 것 같아 여기에 남겨본다.

  - ```text
    우선 1<<n은 주어진 배열의 숫자로 만들 수 있는 총 부분집합의 가지수를 이야기한다. 예를 들어 배열에 담긴 숫자가 5개라면 공집합을 포함한 모든 부분집합의 개수는 32가지가 나온다.
    때문에 맨처음 for문을 1<<n 만큼 돌린다는 의미는 부분집합의 가지수 전체를 출력하겠다는 의미이다.
    이후 그 밑에 for문(이중 for문)을 다시 배열의 길이만큼 돌려 &을 활용해 이를 이진법으로 표현했을 때(컴퓨터에서의 비트연산자는 이진법이므로)를 배열의 index로 활용한다.
    무슨 말이냐면, 배열안에 있는 모든 수를 이진수로 표현하면 1에 해당하는 자리 수는 곂칠일이 없다. 때문에 이를 그대로 index 값으로 활용해 주면 배열안에 곂치지 않고 모든 경우의 수가 출력된다는 의미이다.
    이 정도까지 비트연산자 부분집합을 혼자 연습해보며 알아냈는데, 덕분에 코드를 짜면서도 몬가 괴리감을 줄이고 내꺼라는 느낌이 들 수 있었다.
    ```

    