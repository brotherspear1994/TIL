# swea

# 영준이의 카드 카운팅

### 일자 20200902

### 문제

최근 영준이는 카드 게임에 꽂혀 있다.

영준이가 하는 카드 게임에는 한 덱의 카드가 필요한데 여기서 얘기하는 “한 덱”이란 스페이드, 다이아몬드, 하트, 클로버 무늬 별로 각각 A, 2~10, J, Q, K의 라벨 즉 4개의 무늬 별로

각각 13장씩 총 52장의 카드가 있는 모음을 의미한다.

편의상 A는 1, J, Q, K는 11, 12, 13으로 하여 1~13의 숫자가 카드에 적혀있다고 하자.

영준이는 몇 장의 카드를 이미 가지고 있는데 게임을 하기 위해서 몇 장의 카드가 더 필요한지 알고 싶어 한다.

그리고 이미 겹치는 카드를 가지고 있다면 오류를 출력하고자 한다.

지금 가지고 있는 카드의 정보가 주어지면 이 작업을 수행하는 프로그램을 작성하라.


**[입력]**

맨 위 줄에 테스트케이스의 개수가 주어진다.

각 테스트케이스 별로 순서대로 첫 번째 줄에 지금 영준이가 가지고 있는 카드에 대한 정보 S (1 ≤ |S| ≤ 1000)가 주어진다.

S는 각각 3자리로 표현되는 카드들의 정보를 붙여서 만든 하나의 문자열인데 각 카드는 TXY 꼴로 표현되며,

T는 카드의 무늬(S, D, H, C)이며 XY는 카드의 숫자 (01 ~ 13)이다.

**[출력]**

각 테스트케이스 별로 순서대로 한 줄씩 답을 출력하는데, 문자열 S를 보고 지금 무늬 별로(S, D, H, C 순서로) 몇 장의 카드가 부족한지 출력하여라.

이미 겹치는 카드가 있다면 문자열 “ERROR” (쌍따옴표는 출력하지 않는다)를 출력한다
 

#### 풀이1

```python
'''
3
S01D02H03H04S02
H02H10S11H02
S10D10H10C01
'''

def deQueue():
    return Q.pop(0)

T = int(input())
for tc in range(1,T+1):
    card_info = input()
    Q = []
    for i in range(0,len(card_info),3):
        Q.append(card_info[i:i+3])
    # print(Q)
    S, D, H, C = 0, 0, 0, 0
    A = 13
    bool = True
    while Q:
        pop_card = deQueue()
        if pop_card in Q: print("#{} ERROR".format(tc)); bool=False; break
        else:
            if pop_card[0] == 'S': S += 1
            if pop_card[0] == 'D': D += 1
            if pop_card[0] == 'H': H += 1
            if pop_card[0] == 'C': C += 1
    if bool == True: print("#{} {} {} {} {}".format(tc, A-S, A-D, A-H, A-C))


```

### 풀이 2

```python
'''
3
S01D02H03H04S02
H02H10S11H02
S10D10H10C01
'''
T = int(input())
for tc in range(1,T+1):
    # 카드 한덱을 저장하기 위한 배열 선언
    deck = [[0 for _ in range(13)] for _ in  range(4)]
    types = ["S","D","H","C"]
    cards = list(input())
    # print(cards)

    # 리스트에서 한장씩 꺼내서 작업
    # 리스트에서 자료가 있는 동안 + 에러가 없는 동안
    isError = False
    while cards and not isError:
        type = cards.pop(0)
        nums = cards.pop(0)
        nums = nums + cards.pop(0)
        num = int(nums)

        for i in range(len(types)):
            if type == types[i]:
                if deck[i][num] == 0: # 아직 카드가 없을떄
                    deck[i][num] = 1
                else: isError = True; break # 에러발생 체크

    print("#%s"%tc, end=' ')
    if isError:
        print("ERROR")
    else:
        for row in deck:
            need = 0 # 필요한 카드수 세기(무늬별)
            for c in row:
                if c == 0:need += 1
            print(need, end=" ")
        print()
```

- Queue를 학습한 직후 Queue 알고리즘을 활용하는 문제를 바로 풀어보았다.
- 풀이 1은 Queue를 학습한 직후 혼자 풀어본 풀이 방식이고 풀이 2는 이후 일주일 후 쯤 교수님이 풀이해준 풀이 방식이다.
- 교수님의 풀이 이후 이해를 한후 혼자 코딩을 다시 짜보는 시간을 가졌다.