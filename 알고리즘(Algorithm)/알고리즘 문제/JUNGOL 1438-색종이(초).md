# JUNGOL

# 1438 : 색종이(초)

### 문제

가로, 세로의 크기가 각각 100인 정사각형 모양의 흰색 도화지가 있다.

이 도화지 위에 가로, 세로의 크기가 각각 10인 정사각형 모양의 검은색 색종이를 색종이의 변과 도화지의 변이 평행하도록 붙인다. 

이러한 방식으로 색종이를 한 장 또는 여러 장 붙인 후 색종이가 붙은 검은 영역의 넓이를 구하는 프로그램을 작성하시오.

 

![img](http://jungol.co.kr/data/editor/1512/e3050b66a1b29a01767400d7560a4131_1449727465_3801.png)



예를 들어 흰색 도화지 위에 세 장의 검은색 색종이를 그림과 같은 모양으로 붙였다면 검은색 영역의 넓이는 260이 된다.



### 입력형식

첫째 줄에 색종이의 수가 주어진다. 이어 둘째 줄부터 한 줄에 하나씩 색종이를 붙인 위치가 주어진다.

색종이를 붙인 위치는 두 개의 자연수로 주어지는데 첫 번째 자연수는 색종이의 왼쪽 변과 도화지의 왼쪽 변 사이의 거리이고, 두 번째 자연수는 색종이의 아래쪽 변과 도화지의 아래쪽 변 사이의 거리이다. 

색종이의 수는 100 이하이며, 색종이가 도화지 밖으로 나가는 경우는 없다.



### 풀이

```python
'''
3 
3 7 
15 7 
5 2
'''
# 입력
maps = [[0]*100 for _ in range(100)]

paper_num = int(input())
for coloring in range(paper_num):
    x, y = map(int,input().split())
    for row in range(y,y+10):
        for column in range(x,x+10):
            maps[row][column] = 1
            
#출력

# cnt = 0
# for i in range(len(maps)):
#     for j in range(len(maps[0])):
#         if maps[i][j] == 1:
#             cnt += 1
# print(cnt)
cnt = 0
for i in maps:
    cnt += i.count(1)
print(cnt)
```



- 출력형식을 일부로 두가지로 만들어 보았다. 후자가 코드가 더 단순하고 직관적이어서 후자를 선택해 보았다. ㅎㅎ