# swea

# Magnetic

### 일자 20200901



### 문제

[본문 링크 참조](https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AV14hwZqABsCFAYD&categoryId=AV14hwZqABsCFAYD&categoryType=CODE)

테이블 위에 자성체들이 놓여 있다.

자성체들은 성질에 따라 색이 부여되는데, 푸른 자성체의 경우 N극에 이끌리는 성질을 가지고 있고, 붉은 자성체의 경우 S극에 이끌리는 성질이 있다.

테이블에서 일정 간격을 두고 강한 자기장을 걸었을 때, 시간이 흐른 뒤에 자성체들이 서로 충돌하여 테이블 위에 남아있는 교착 상태의 개수를 구하라.

**[제약 사항]**

자성체는 테이블 앞뒤 쪽에 있는 N극 또는 S극에만 반응하며 자성체끼리는 전혀 반응하지 않는다.

테이블의 크기는 100x100으로 주어진다. (예시에서는 설명을 위해 7x7로 주어졌음에 유의)

**[입력]**

각 테스트 케이스의 첫 번째 줄에는 정사각형 테이블의 한 변의 길이가 주어진다. 그리고 바로 다음 줄에 테스트 케이스가 주어진다.

총 10개의 테스트 케이스가 주어진다.

1은 N극 성질을 가지는 자성체를 2는 S극 성질을 가지는 자성체를 의미하며 테이블의 윗 부분에 N극이 아랫 부분에 S극이 위치한다고 가정한다.

**[출력]**

\#부호와 함께 테스트 케이스의 번호를 출력하고, 공백 문자 후 교착 상태의 개수를 출력한다.

#### 풀이

```python
def S_move(i,j):
    global move
    table[i][j] = 0
    if i-1 < 0: return
    elif table[i-1][j] == 2 or table[i-1][j] == 1: table[i][j] = 2; return
    elif table[i-1][j] == 0: table[i-1][j] = 2; move += 1; return

def N_move(i,j):
    global move
    table[i][j] = 0
    if i+1 >= N: return
    elif table[i+1][j] == 2 or table[i+1][j] == 1: table[i][j] = 1; return
    elif table[i+1][j] == 0: table[i+1][j] = 1; move += 1; return

def count(i,j):
    global cnt
    if table[i+1][j] == 2: cnt +=1; table[i][j] = 0; table[i+1][j] = 0; return
    else: return

for tc in range(1,11):
    N = int(input())
    table = [list(map(int,input().split())) for _ in range(N)]
    # for row in table:
    #     print(row)
    # print()
    move = 1
    while move > 0:
        move = 0
        for i in range(N):
            for j in range(N):
                if table[i][j] == 1: N_move(i,j)
                elif table[i][j] == 2: S_move(i,j)
    # for row in table:
    #     print(row)
    # print()
    cnt = 0
    for a in range(N):
        for b in range(N):
            if table[a][b] == 1: count(a,b)
    print("#{} {}".format(tc, cnt))
```

- 이 문제를  풀었을 당시, 아직 Queue를 안배우고 막 Stack만 배우고 난 후로 기억난다.
- 지금 문제와 코드를 보니 이 문제는 시뮬레이션 문제에 가깝다는 생각이 든다.
- 시뮬레이션은 어려운 난이도에 속하나, 당시 배웠던 내용안에서 충분히 구현해 낼 수 있어 아마 풀었던 기억이 난다.