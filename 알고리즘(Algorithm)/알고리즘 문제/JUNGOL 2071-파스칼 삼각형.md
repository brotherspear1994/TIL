# JUNGOL

# 2071: 파스칼삼각형

### 문제

[홈페이지 문제 본문참조](http://jungol.co.kr/bbs/board.php?bo_table=pbank&wr_id=1335&sca=2020)

```python
n, m = map(int, input().split())
if m == 1:
    arr_1 = []
    for row_1 in range(1,n+1):
        arr_1.append([0]*row_1)
    
    arr_1[0][0] = 1
    for x_1 in range(1,n):
        for y_1 in range(x_1+1):
            if y_1 == 0:
                arr_1[x_1][y_1] = 1
            elif y_1 == x_1:
                arr_1[x_1][y_1] = 1
            else:
                arr_1[x_1][y_1] = arr_1[x_1-1][y_1-1] + arr_1[x_1-1][y_1]

    for i_1 in range(len(arr_1)):
        for j_1 in arr_1[i_1]:
            print(j_1, end=' ')
        print()

if m == 2:
    arr_1 = []
    for row_1 in range(1,n+1):
        arr_1.append([0]*row_1)
    
    arr_1[0][0] = 1
    for x_1 in range(1,n):
        for y_1 in range(x_1+1):
            if y_1 == 0:
                arr_1[x_1][y_1] = 1
            elif y_1 == x_1:
                arr_1[x_1][y_1] = 1
            else:
                arr_1[x_1][y_1] = arr_1[x_1-1][y_1-1] + arr_1[x_1-1][y_1]
    for x in range(n):
        if x % 2 == 0:
            arr_1[x] = [' ']*int((n-x)//2) + arr_1[x] + [' ']*int((n-x)//2)
        elif x == 1:
            arr_1[x] = ['  ']*(int((n-x)//2)-1) + arr_1[x] + [' ']*int((n-x)//2)
        else:
            arr_1[x] = ['']*int((n-x)//2) + arr_1[x] + ['']*int((n-x)//2)
    # 출력
    for x in range(n):
        for y in range(len(arr_1[x])):
            print(arr_1[x][y], end=' ')
        print()
      
```



- 유형 2까지 풀었지만, 파스칼 삼각형 모양이 입력받은 n의 값에 따라 정바르게 나오기도하고 일그러지게 나오기도 한다. 시간을 더 들이면 풀수 있을것 같기도 하지만, 우선 시간이 촉박하고, 코딩도 깔끔하지 못해 본래 이렇게 푸는 방식이 아닌 것 같다. 교수님께 개인질문을 드려야할 것 같다.