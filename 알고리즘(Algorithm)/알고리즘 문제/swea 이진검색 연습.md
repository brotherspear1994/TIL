# swea

# 이진검색 연습문제

### 일자 20200805

#### 풀이

```python
def bin_search(a, key):
    start =0
    end = len(a)
    print(end)
    while start <= end:
        middle = (start + end) //2
        if a[middle] == key:
            print(middle)
            print(a[middle])
            return True
        elif a[middle] > key:
            end = middle - 1
        else:
            start = middle + 1

arr = [2,4,7,9,11,19,23]
key = 7
print(bin_search(arr, key))
```



- 주어진 리스트에서 내가 원하는 값의 존재유무를 이진검색을 통해 찾아내는 연습을 했다.

- 리스트의 index를 반으로 쪼개가며 못찾을때 마다 동일한 행위를 반복해 값이 있다면 True를 없다면 False를 return하게 했다.

  