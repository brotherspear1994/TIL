# SWEA

# 이진수 1, 2

### 일자 20201027

#### 문제

#### SWEA 이진수1

#### 풀이

```python
'''
3
4 47FE
5 79E12
8 41DA16CD
'''
for tc in range(1,int(input())+1):
    N, hexa = map(str, input().split())
    N = int(N)
    digit = []
    for i in range(N):
        d = ord(hexa[i]) - ord('0') if '0' <= hexa[i] <= '9' else ord(hexa[i]) - ord('A') + 10
        # print(d)
        output = ""
        for j in range(3,-1,-1):
            output += '1' if d & (1<<j) else '0'
        for k in range(len(output)):
            digit.append(int(output[k]))

    print("#{}".format(tc), end=' ')
    for h in digit:
        print(h, end='')
    print()

```

- 십진수를 입력값으로 받고 이를 for문, if문 구조, 비트연산자를 활용하여 이진수로 변환하는 문제이다.

#### 문제

#### SWEA 이진수2

#### 풀이

```python
'''
3
0.625
0.1
0.125
'''
def find(lst, idx, acc):
    global finded
    if acc == N:
        finded = True
        print("#{}".format(tc), end=' ')
        for j in range(1,idx):
            print(lst[j], end='')
        print()
        return
    elif idx == 13:
        return
    lst[idx] = 1
    find(lst, idx+1, acc+(1*(2**(-idx))))
    lst[idx] = 0
    find(lst, idx + 1, acc)

for tc in range(1,int(input())+1):
    N = float(input())

    finded = False
    binary = [0]*13
    find(binary, 1, 0)
    if not finded:
        print("#{} overflow".format(tc))
```

- 소수값이 주어졌을때 이진수로 변환시킬 수 있는지 물어보는 문제였다.
- 나는 다른 사람들이 보통 푸는 방식과는 약간 다르게 dfs 재귀 함수로도 문제를 풀어보았다.