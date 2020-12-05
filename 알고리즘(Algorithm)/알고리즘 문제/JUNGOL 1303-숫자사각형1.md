# JUNGOL

# 1303 : 숫자사각형1

### 문제

사각형의 높이 n과 너비 m을 입력받은 후 

n행 m열의 사각형 형태로 1부터 n*m번까지 숫자가 차례대로 출력되는 프로그램을 작성하시오.

< 처리조건 >
숫자의 진행 순서는 처음에 맨 윗줄의 왼쪽에서 오른쪽으로 1부터 차례대로 너비 m만큼 출력한 후 

다음 줄로 바꾸어서 다시 왼쪽에서 오른쪽으로 1씩 증가하면서 출력하는 방법으로 n번 줄까지 반복한다.

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
    for y in range(m):
        arr[x][y] = (y+1)+(x*m)
# print(arr)
# 출력
for i in range(len(arr)):
    for j in arr[i]:
        print(j, end= ' ')
    print()         

```



- 비교적 쉽게 빨리 풀수 있었다.
- 계산에서 굳이 어렵게 구하지 않고 배열안에서 규칙성을 찾아내 간단히 풀어내려고 했다.