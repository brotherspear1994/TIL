# JUNGOL

# 1856 : 숫자사각형2

### 문제

사각형의 높이 n과 너비 m을 입력받은 후 

사각형 내부에 지그재그 형태로 1부터 n*m번까지 숫자가 차례대로 출력되는 프로그램을 작성하시오. 

 

**< 처리조건 >** 

숫자의 진행 순서는 처음에 왼쪽에서 오른쪽으로 너비 m만큼 진행 한 후 방향을 바꾸어서 이를 반복한다.

```python
#입력
n, m = map(int, input().split())
# print(m)

# arr = []
# for _ in range(n):
#     arr.append([0]*m)
# print(arr)
#계산
arr = [[0]*m for _ in range(n)]
for x in range(n):
    if x % 2 ==0:
        for y in range(m):
            arr[x][y] = (y+1)+(x*m)
    else:
        for y in range(m-1,-1,-1):
            arr[x][y] = (m-y)+(x*m)

# print(arr)
# 출력
for i in range(len(arr)):
    for j in arr[i]:
        print(j, end= ' ')
    print()         

```



- 바로 이전의 숫자사각형1과 연계된 문제이다.
- if조건문으로 계산의 구획을 나누어 지그재그 형태의 사각형이 되게끔 만들었고, 이번에 마찬가지로 배열안에서 규칙성을 찾아내 코딩수식을 최대한 간단히 만드려고 노력했다.