# JUNGOL

## 165 : 배열2 - 형성평가6

### 문제

예제를 보고 적당한 배열을 선언한 후 1행의 1열과 3열 5열을 각각 1로 초기화하고 나머지는 모두 0으로 초기화 한 후 2행부터는 바로 위행의 왼쪽과 오른쪽의 값을 더하여 채운 후 출력하는 프로그램을 작성하시오.

```python
arr = [[0]*5 for line in range(5)]
for i in range(len(arr[0])):
    for j in range(len(arr[0])):
        if i == 0:
            if not j % 2:
                arr[i][j] += 1
        if i % 2:
            if j % 2:
                arr[i][j] = arr[i-1][j-1] + arr[i-1][j+1]
            else:
                pass
        if i % 2==0 and i>0:
            if j % 2==0 and j<4:
                arr[i][j] = arr[i-1][j-1] + arr[i-1][j+1]
            elif j ==4:
                arr[i][j] = arr[i-1][j-1]
            else:
                pass

            
for i in range(len(arr)):
    for j in range(len(arr)):
        print(str(arr[i][j]), end=' ')
    print()
```



- 다른 함수를 사용하지 않고 for문 반복만으로 풀었다.
- 출력형식을 맞추느라 애먹었다.. 출력형식 맞추기에 다른 방법이 있는지 알아봐야겠다.