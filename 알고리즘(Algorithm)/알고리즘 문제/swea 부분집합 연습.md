# swea

# 부분집합 연습문제

### 일자 20200805

#### 풀이

```python
# 비트연산자
arr = [1,2,3]

N = len(arr)

for i in range(1<<N):
    # print(i)
    for j in range(N):
```



```python
# 비트연산자를 활용해 부분집합 뽑아내기
arr = [1,2,3]
n = len(arr)
# print(1<<n) #부분집합 총 개수

for i in range(1<<n):
    # print(i)
    list_m =[]
    for j in range(n):
        # print(j)
        # if i&(1<<j):
        print(i&(1<<j),end= ',')
    print()
```

- 주어진 리스트 안에서 모든 부분집합을 print하는 연습을 했다.

- 지금은 비트연산자를 활용해 각 경우의수를 표현하는 비트들이 중복되지 않는다는 점을 활용하여, 그 비트에 해당하는 index 부분만 프린트하면 자연스럽게 모든 경우의수가 나온다는 것을 잘 알지만 당시에는 이해하기 꽤 어려운 개념이었다. 

  