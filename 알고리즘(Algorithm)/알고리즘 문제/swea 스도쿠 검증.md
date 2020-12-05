# swea

# 스도쿠검증

### 일자 20200825

### 문제

스도쿠는 숫자퍼즐로, **가로 9칸 세로 9칸**으로 이루어져 있는 표에 **1 부터 9 까지의 숫자**를 채워넣는 퍼즐이다.





같은 줄에 **1 에서 9 까지의 숫자를 한번씩만 넣고, 3 x 3 크기의 작은 격자 또한, 1 에서 9 까지의 숫자가 겹치지 않아야 한다.**





입력으로 9 X 9 크기의 스도쿠 퍼즐의 숫자들이 주어졌을 때, 위와 같이 겹치는 숫자가 없을 경우, 1을 정답으로 출력하고 그렇지 않을 경우 0 을 출력한다.


**[제약 사항]**

\1. 퍼즐은 모두 숫자로 채워진 상태로 주어진다.

\2. 입력으로 주어지는 퍼즐의 모든 숫자는 1 이상 9 이하의 정수이다.


**[입력]**

입력은 첫 줄에 총 테스트 케이스의 개수 T가 온다.

다음 줄부터 각 테스트 케이스가 주어진다.

테스트 케이스는 9 x 9 크기의 퍼즐의 데이터이다.


**[출력]**

테스트 케이스 t에 대한 결과는 “#t”을 찍고, 한 칸 띄고, 정답을 출력한다.

(t는 테스트 케이스의 번호를 의미하며 1부터 시작한다.)

#### 풀이

```python
T = int(input())
for tc in range(1, T+1):
    arr = [list(map(int, input().split())) for _ in range(9)]
    result = 1
    # 가로
    for i in range(9):
        bool_set = set()
        for j in range(9):
            bool_set.add(arr[i][j])
        if len(bool_set) != 9:
            result = 0
            break
    # 세로
    for i in range(9):
        lst_sub = []
        for j in range(9):
            lst_sub.append(arr[j][i])
        if len(set(lst_sub)) != 9:
            result = 0
            break
    #정사각형
    for a in range(3):
        for b in range(3):
            set_sub = set()
            for r in range(3*a, 3*(a+1)):
                for c in range(3*b, 3*(b+1)):
                    set_sub.add(arr[r][c])
            if len(set_sub) != 9:
                result = 0
                break
    print("#{} {}".format(tc, result))
```

- 우선 for문을 전체 가로줄, 전체 세로줄, 3X3크기의 정사각형의 스도쿠 존재 유무를 모두 검증할 수 있게 출발점과 종료점을 적절히 설정해 줄 수 있는 것이 중요하다.
- 그 다음 스도쿠 검증 함수를 짜 각 출발점마다 함수를 실행해 스도쿠 존재유무를 확인한다.
- 당시에는 코딩을 배우진 채 1달이 되지 않은 시점이었기 때문에 문제를 푸는데 어려움을 겪은 기억이 난다. 
- 교수님의 문제풀이를 듣고 나 혼자 풀어보는 연습도 당연히 가졌다.

