# swea

# 배열 순회

### 일자 20200805

#### 풀이

```python
arr = [ [1,2,3],
        [4,5,6],
        [7,8,9]
       ]

N = len(arr) #행의 길이
M = len(arr[0])

#행우선
# for in range(N):
#     for j in range(M):
#         print(arr[i][j], end=" ")
#     print()
# print()

#열우선
for j in range(M):
    for i in range(N):
        print(arr[i][j], end=" ")
    print()
print()
```

- 주어진 배열을 완전히 순회하며 각 행을 기준으로 print하는 연습을 했다.

  