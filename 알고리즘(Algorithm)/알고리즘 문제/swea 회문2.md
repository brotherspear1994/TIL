# swea

# 회문2

### 일자 20200825

### 문제

### 1216. [S/W 문제해결 기본] 3일차 - 회문2

[본문 링크 참조](https://swexpertacademy.com/main/solvingProblem/solvingProblem.do#collapseOne)

"기러기" 또는 "level" 과 같이 거꾸로 읽어도 제대로 읽은 것과 같은 문장이나 낱말을 회문(回文, palindrome)이라 한다.

주어진 100x100 평면 글자판에서 가로, 세로를 모두 보아 가장 긴 회문의 길이를 구하는 문제이다.



**[제약사항]**

각 칸의 들어가는 글자는 c언어 char type으로 주어지며 'A', 'B', 'C' 중 하나이다.

글자 판은 무조건 정사각형으로 주어진다.

ABA도 회문이며, ABBA도 회문이다. A또한 길이 1짜리 회문이다.

가로, 세로 각각에 대해서 직선으로만 판단한다. 즉, 아래 예에서 노란색 경로를 따라가면 길이 7짜리 회문이 되지만 직선이 아니기 때문에 인정되지 않는다. 


**[입력]**

각 테스트 케이스의 첫 번째 줄에는 테스트 케이스의 번호가 주어지며, 바로 다음 줄에 테스트 케이스가 주어진다.

총 10개의 테스트케이스가 주어진다.

**[출력]**

\#부호와 함께 테스트 케이스의 번호를 출력하고, 공백 문자 후 찾은 회문의 길이를 출력한다.

#### 풀이

```python
for _ in range(1, 11):
    tc = int(input())
    result = []

    Garo_lst = []
    for _ in range(100):
        Data = input()
        Garo_lst.append(Data)
        for M in range(2,len(Data)+1):
            for i in range(len(Data)-M+1):
                if Data[i:i+M] == Data[i:i+M][::-1]:
                    result.append(Data[i:i+M])
    # print(result)

    # 세로
    Sero_lst = []
    Sero_lst_sub = ''
    for x in range(100):
        for y in range(100):
            Sero_lst_sub += Garo_lst[y][x]
        Sero_lst.append(Sero_lst_sub)
        Sero_lst_sub = ''
    # print(Sero_lst)
    for Sero_data in Sero_lst:
        for M in range(2, len(Sero_data)+1):
            for i in range(len(Sero_data)-M+1):
                if Sero_data[i:i+M] == Sero_data[i:i+M][::-1]:
                    result.append(Sero_data[i:i+M])
    max_len = 0
    for i in result:
        if len(i) > max_len:
            max_len = len(i)
    print('#%s %s'%(tc, max_len))
```



### 풀이2

```python
def find(row, start, end):
    global cnt
    len = end - start + 1
    half = len//2 if len % 2 == 0 else len//2+1

    s = []
    for i in range(start, start+half):
        s.append(map[row][i])
    if len % 2 == 1:
        s.pop()
    if len != 1:
        for i in range(start+half, end+1):
            if s.pop() != map[row][i]:
                return
    # 회문발견함
    if cnt < len:
        cnt = len


T = 10
N = 100
for tc in range(1,T+1):
    int(input())
    map = [list(input()) for _ in range(N)]
    # print(map)
    # 세로방향으로 배열 추가하기
    for i in range(N):
        temp = []
        for j in range(N):
            temp.append(map[j][i])
        map.append(temp)
    # for row in map:
    #     print(row)

    cnt = 0
    for i in range(2*N):
        for j in range(N):
            for k in range(j,N):
                if k-j+1 > cnt :
                    find(i,j,k)
    print('#{} {}'.format(tc, cnt))
```



- 회문1 문제와 거의 유사한 문제이다.
- 당시에 회문1을 어렵게 풀어 교수님의 답안 풀이를 한번 더 보고 그 방법을 적용해 회문2를 혼자 풀어보려했던 기억이 난다.
- 회문1과 크게 다르지 않아 결론적으로는 쉽게 풀어낼 수 있었다.
- 이후에는 스택개념을 학습한 후, 이를 활용해 회문2문제를 풀어보는 시간도 가졌다.
- 이때는 교수님의 풀이도 본 후에 이를 혼자서 연습해보는 시간도 가졌다.