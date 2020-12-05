# swea

# Ladder2

### 일자 20200827

### 문제

점심 시간에 산책을 다니는 사원들은 최근 날씨가 더워져, 사다리 게임을 통하여 누가 아이스크림을 구입할지 결정하기로 한다.

김 대리는 사다리타기에 참여하지 않는 대신 사다리를 그리기로 하였다.

사다리를 다 그리고 보니 김 대리는 어느 사다리를 고르면 X표시에 도착하게 되는지 궁금해졌다. 이를 구해보자.

아래 <그림 1>의 예를 살펴보면, 출발점 x=0 및 x=9인 세로 방향의 두 막대 사이에 임의의 개수의 막대들이 랜덤 간격으로 추가되고(이 예에서는 2개가 추가됨) 이 막대들 사이에 가로 방향의 선들이 또한 랜덤하게 연결된다.

X=0인 출발점에서 출발하는 사례에 대해서 화살표로 표시한 바와 같이, 아래 방향으로 진행하면서 좌우 방향으로 이동 가능한 통로가 나타나면 방향 전환을 하게 된다.

방향 전환 이후엔 다시 아래 방향으로만 이동하게 되며, 바닥에 도착하면 멈추게 된다.

문제의 X표시에 도착하려면 X=4인 출발점에서 출발해야 하므로 답은 4가 된다. 해당 경로는 별도로 표시하였다.
 

![img](swea 스도쿠 검증.assets/fileDownload.do)

<그림 1> 사다리 게임에 대한 설명(미니맵)


아래 <그림 2>와 같은 **100 x 100 크기의 2차원 배열로 주어진 사다리에 대해서, 모든 출발점을 검사하여 가장 짧은 이동 거리를 갖는 시작점 x(복수 개인 경우 가장 큰 x좌표)를 반환하는 코드를 작성하라.**(‘0’으로 채워진 평면상에 사다리는 연속된 ‘1’로 표현된다. 도착 지점은 '2'로 표현된다.)
 

 ![img](swea 스도쿠 검증.assets/fileDownload.do)

<그림 2> 테스트케이스에 의해 생성되는 실제 사다리의 모습

 
**[제약사항]**

한 막대에서 출발한 가로선이 다른 막대를 가로질러서 연속하여 이어지는 경우는 없다.

**[입력]**

각 테스트 케이스의 첫 번째 줄에는 테스트 케이스의 번호가 주어지며, 바로 다음 줄에 테스트 케이스가 주어진다.

총 10개의 테스트 케이스가 주어진다.

**[출력]**

\#부호와 함께 테스트 케이스의 번호를 출력하고, 공백 문자 후 도착하게 되는 출발점의 x좌표를 출력한다.



#### 풀이

```python
for tc in range(1,11):
    _ = int(input())
    ladder = [list(map(int,input().split())) for _ in range(100)]
    # for row in ladder:
    #     print(row)
    # 시작점 스텍 쌓기
    start_stack = []
    for i in range(len(ladder[0])):
        if ladder[0][i] == 1:
            start_stack.append(i)
    # print(start_stack)
    s = start_stack[0]
    y = 0
    cnt_sub = 0
    min_idx = 0

    min = 10000


    while 1:
        # 오른쪽 이동
        if s < 99 and ladder[y][s+1] != 0:
            while s < 99 and ladder[y][s+1] != 0:
                s += 1
                cnt_sub += 1
            else:
                y += 1
                cnt_sub += 1
        # 왼쪽 이동
        elif s > 0 and ladder[y][s-1] != 0:
            while s > 0 and ladder[y][s-1] != 0:
                s -= 1
                cnt_sub += 1
            else:
                y += 1
                cnt_sub += 1
        else:
            y += 1
            cnt_sub += 1
        if y == 99 and len(start_stack) > 1:
            if cnt_sub < min:
                min = cnt_sub
                min_idx = start_stack[0]
            start_stack.pop(0)
            y = 0
            s = start_stack[0]
            cnt_sub = 0
        if y == 99 and len(start_stack) == 1:
            if cnt_sub < min:
                min = cnt_sub
                min_idx = start_stack[0]
            break
    print("#{} {}".format(tc, min_idx))
```

-  SWEA의 Ladder1 문제와 유사해 보이나, 이 문제는 stack을 활용해 사다리 타기의 시작점과 이동간 정보를 잘 저장하고 빼내주는 과정이 더 중요한 문제이다.
- Ladder1을 푼 직후 풀은 문제라 그리 어렵지 않게 푼 기억이 난다.

