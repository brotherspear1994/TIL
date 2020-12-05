# swea

# 순차탐색 연습문제

### 일자 20200805

#### 풀이

```python
def seq_search(a, n ,k):
    i = 0
    while i < n and a[i] != k:
        i += 1
    if i < n: return i
    else: return -1


def seq_search(a, n ,k):
    i = 0
    while i < n and a[i] < k:
        i += 1
    if i < n and a[i] == k: return i
    else: return -1


arr = [4, 9, 11, 23, 2, 19, 7]
key = 23

print(seq_search(arr, len(arr), key))
```



- 주어진 리스트에서 원하는 값의 index위치를 찾아내는 함수를 만들어봤다. 만약 찾는 값이 없다면 -1을 표시하도록 함수를 짯다. 어떻게 보면 python의 find기능을 구현해 본 것이라 할 수 있다.

  