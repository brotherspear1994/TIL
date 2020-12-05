# JUNGOL

# 1338 : 문자삼각형1

### 문제

삼각형의 높이 N을 입력받아서 아래와 같이 문자 'A'부터 차례대로 왼쪽 대각선으로 채워서 삼각형 모양을 출력하는 프로그램을 작성하시오.

< 처리조건 >
(1) 오른쪽 위부터 왼쪽 아래쪽으로 이동하면서 문자 'A'부터 차례대로 채워나간다.
(2) N번 행까지 채워지면 다시 오른쪽 둘째 행부터 왼쪽 아래로 채워나간다.
(3) 삼각형이 모두 채워질 때까지 반복하면서 채워 나간다. (문자 'Z'다음에는 'A'부터 다시 시작한다.)

![img](http://jungol.co.kr/data/editor/1512/e3050b66a1b29a01767400d7560a4131_1449726717_0591.png)


```python
#입력
import string
Alpha = list(string.ascii_uppercase)
# print(Alpha)

N = int(input())
arr = [[0]*i for i in range(1,N+1)]
# print(arr)

#계산
idx = 0
for x in range(N):
    for i in range(x,N):
        arr[i][x] = Alpha[idx]
        idx += 1
#출력
# print(arr)
for j in range(N):
    for k in arr[j]:
        print(k, end=' ')
    print()

```



- 알파벳 문자를 받아오는 형식을 배우지 못해 이번기회에 import string한 후 ascii코드를 소문자나 대문자형식의 string으로 받아오는 방법을 학습했다.
- 계산은 수도코드 작성 후 완료했는데, 걸린 시간에 비해 간단한 코드로 완성돼 뿌듯하면서 허탈했다. 다음부터는 시간을 줄일수 있도록 해야겠다. 