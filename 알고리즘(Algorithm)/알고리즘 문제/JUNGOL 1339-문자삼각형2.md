# JUNGOL

# 1339 : 문자삼각형2

삼각형의 높이 N을 입력받아서 아래와 같이 문자 'A'부터 차례대로 맨 오른쪽 가운데 행부터 차례대로 아래와 같이 채워서 

삼각형 모양을 출력하는 프로그램을 작성하시오.

< 처리조건 >
(1) 오른쪽 가운데 행에 문자 'A'를 채우고 왼쪽 열로 이동하여 위에서 아래로 채워나간다.
(2) 가장 왼쪽 행까지 반복하여 모두 채워 나간다. (문자 'Z'다음에는 'A'부터 다시 시작한다.)

![img](http://jungol.co.kr/data/editor/1512/e3050b66a1b29a01767400d7560a4131_1449726750_1992.png)


```python
#입력
import string
Alpha = list(string.ascii_uppercase)
# print(Alpha)

N = int(input())
if N % 2 ==0:   
    arr = [[0]*i for i in range(1,(N//2)+1)] + [[0]*j for j in range(N//2, 0, -1)]
else:
    arr = [[0]*i for i in range(1,(N//2+1)+1)] + [[0]*j for j in range(N//2, 0, -1)]
# print(arr)

# 계산
if N % 2 == 0:
    idx = 0
    for i in range((N//2)-1,-1,-1):
        for j in range(N):
            if i <= j <= N-i-1:
                arr[j][i] = Alpha[idx]
                idx += 1
            else:
                pass
if N % 2 == 1:
    idx = 0
    for i in range((N//2),-1,-1):
        for j in range(N):
            if i <= j <= N-i-1:
                arr[j][i] = Alpha[idx]
                idx += 1
            else:
                pass

# 출력

for x in range(N):
    for y in arr[x]:
        print(y, end=' ')
    print()




```



- 짝수 경우와 홀수 경우를 나누어서 코드를 짜느라 시간이 다소 걸렸다.
- 내 수준에는 꽤 어려웠던것 같은데 온전히 나의 힘으로 풀어내 뿌듯하다. ㅎㅎ 