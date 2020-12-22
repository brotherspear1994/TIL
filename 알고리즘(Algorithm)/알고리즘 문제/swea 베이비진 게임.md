# swea

# 베이비진

### 일자 20201029

#### 문제

0부터 9까지인 숫자 카드 4세트를 섞은 후 6개의 카드를 골랐을 때, 연속인 숫자가 3개 이상이면 run, 같은 숫자가 3개 이상이면 triplet이라고 한다.

게임을 시작하면 플레이어1과 플레이어 2가 교대로 한 장 씩 카드를 가져가며, 6장을 채우기 전이라도 먼저 run이나 triplet이 되는 사람이 승자가 된다.

두 사람이 가져가게 되는 순서대로 12장의 카드에 대한 정보가 주어졌을 때 승자를 알아내는 프로그램을 작성하시오. 만약 무승부인 경우 0을 출력한다.

예를 들어 9 9 5 6 5 6 1 1 4 2 2 1인 경우, 플레이어 1은 9, 5, 5, 1, 4, 2카드를, 플레이어2는 9, 6, 6, 1, 2, 1을 가져가게 된다.

이때는 카드를 모두 가져갈 때 까지 run이나 triplet이 없으므로 무승부가 된다.

#### 풀이1

```python
def babygin_game(player_num, idx):
    global ans
    if player_num & 1:
        player = player1
    else:
        player = player2
    # 카드가 3장이라면(트리플렛)
    if player[idx] == 3:
        ans = player_num
    # 왼쪽자리 비교
    if idx > 1:
        if player[idx] and player[idx-1] and player[idx-2]:
            ans = player_num
    # 오른쪽 자리 비교
    if idx < 8:
        if player[idx] and player[idx+1] and player[idx+2]:
            ans = player_num
    # 양쪽방향 비교
    if 0 < idx < 9:
        if player[idx-1] and player[idx] and player[idx+1]:
            ans = player_num



for tc in range(1,int(input())+1):
    cards = list(map(int, input().split()))
    player1 = [0]*10
    player2 = [0]*10
    ans = 0
    for i in range(12):
        if i & 1: # 홀수번째 i
            player2[cards[i]] += 1
            babygin_game(2, cards[i])
        else: # 짝수번째 i
            player1[cards[i]] += 1
            babygin_game(1, cards[i])

        if ans: break
    print("#{} {}".format(tc, ans))
```

- 탐욕 알고리즘의 베이비진 문제이지만, 의외로 재귀함수가 아닌 for문을 이용해 플레이어의 순서를 잘 구분하고, 한번 카드를 놓을때마다 트리플 셋 혹은 run이 났는지 체크해주는 과정만 잘 짜면 된다.

- 문제 자체를 잘 읽고 카드를 놓을때마다 발생할 수 있는 경우의 수를 잘 체크해 주는 것이 중요하다.


#### 풀이2

```python
'''
3
9 9 5 6 5 6 1 1 4 2 2 1
5 3 2 9 1 5 2 0 9 2 0 0
2 8 7 7 0 2 2 2 5 4 0 3
'''
def sort(lst):
    i = 0
    while i < len(lst):
        for j in range(i+1,len(lst)):
            if lst[i] > lst[j]: lst[i], lst[j] = lst[j], lst[i]
        i += 1
    return lst


def run(s_one,s_two):
    global ans; global run_bool
    one_bool = False; two_bool = False
    one_cnt, two_cnt = 0, 0
    one_stack, two_stack = [], []
    for i in range(1, len(s_one)):
        if s_one[i-1] < s_one[i]:
            one_cnt += 1
        else:
            one_stack.append(one_cnt)
            one_cnt = 0
    for j in range(1, len(s_two)):
        if s_two[j-1] < s_two[j]:
            two_cnt += 1
        else:
            two_stack.append(two_cnt)
            two_cnt = 0
    o, t = max(one_stack), max(two_stack)
    if o >= 3: one_bool = True; run_bool = True
    if t >= 3: two_bool = True; run_bool = True

    if one_bool and not two_bool: ans = 1
    if not one_bool and two_bool: ans = 2
    if one_bool and two_bool: ans = 0


def triplet(s_one, s_two):
    global ans; global triplet_bool
    one_bool = False; two_bool = False
    one_cnt, two_cnt = 0, 0
    one_stack, two_stack = [], []
    for i in range(1, len(s_one)):
        if s_one[i-1] == s_one[i]:
            one_cnt += 1
        else:
            one_stack.append(one_cnt)
            one_cnt = 0
    for j in range(1, len(s_two)):
        if s_two[j-1] == s_two[j]:
            two_cnt += 1
        else:
            two_stack.append(two_cnt)
            two_cnt = 0
    o, t = max(one_stack), max(two_stack)
    if o >= 3: one_bool = True; triplet_bool = True
    if t >= 3: two_bool = True; triplet_bool = True

    if one_bool and not two_bool: ans = 1
    if not one_bool and two_bool: ans = 2
    if one_bool and two_bool: ans = 0


def game_start(k,one,two):
    global run_bool; global triplet_bool
    if run_bool or triplet_bool:
        return
    if len(one) >=3 and len(two) >=3 and len(one) == len(two):
        s_one, s_two = sort(one), sort(two)
        run(s_one, s_two)
        triplet(s_one, s_two)
        print(ans)
    if k == 12:
        return
    game_start(k+2,one,two)
    one.append(cards[k])
    game_start(k+2,one,two)
    one.pop()
    two.append(cards[k+1])
    game_start(k+2,one,two)
    one.append(cards[k])
    game_start(k+2,one,two)


for tc in range(1,int(input())+1):
    cards = list(map(int, input().split()))
    # print(cards)
    one = []
    two = []
    ans = 0
    run_bool = False
    triplet_bool = False
    game_start(0,one,two)
```

- 내가 직접 풀어 본 베이비진 게임 풀이

