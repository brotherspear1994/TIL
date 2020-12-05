# JUNGOL

# 168: 배열2 - 형성평가9

### 문제

행의 크기를 입력받아 파스칼 삼각형을 작성하여 마지막 행부터 첫 번째 행까지 역삼각형 모양의 파스칼 삼각형을 출력하시오. 행의 크기는 최대 10이다.

```python
  # 입력
T = int(input())
arr = []
for tc in range(1, T+1):
    arr.append([0] * tc)
# print(arr)

  # 계산
arr[0][0] = 1
for x in range(1, T):
    for y in range(x+1):
        if y == 0:
            arr[x][y] = 1
        elif y == x:
            arr[x][y] = 1
        else: 
            arr[x][y] = arr[x-1][y-1] + arr[x-1][y]
# print(arr)
  #출력
for i in range(len(arr)-1, -1, -1):
    for j in arr[i]:
        print(j, end=' ')
    print()


```



- y의 범위를 잡을때 처음 T로 두어서 지속해서 list index out of range 오류가 발생했다. 매우 쉬운 부분이었음에도 불구하고 실수를 했는데 직접실수를 찾고 해결하는 연습을 해야겠다.