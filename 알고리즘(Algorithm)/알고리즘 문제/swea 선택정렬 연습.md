# swea

# 선택정렬 연습문제

### 일자 20200805

#### 풀이

```python
def selection(a, k):
    for i in range(k):
        min = i
        for j in range(i+1, len(a)):
            if a[min] < a[j]:
                min = j

        a[i], a[min] = a[min], a[i]
        return a[k-1]

def selectionSort(a):
    for i in range(len(a)-1):
        min = i
        for j in range(i+1, len(a)):
            if a[min] > a[j]:
                min = j

        a[i], a[min] = a[min], a[i]

arr = [64, 25, 10, 22, 11]
selectionSort(arr)
print(arr)
print(selection(arr,3))
```



- 주어진 리스트를 내림차순, 혹은 오름차순으로 정렬해 중위값을 뽑아내는 연습을 했다.

  