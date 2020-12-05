# swea

# 베이비진

### 일자 20201029

#### 문제

0부터 9까지인 숫자 카드 4세트를 섞은 후 6개의 카드를 골랐을 때, 연속인 숫자가 3개 이상이면 run, 같은 숫자가 3개 이상이면 triplet이라고 한다.

게임을 시작하면 플레이어1과 플레이어 2가 교대로 한 장 씩 카드를 가져가며, 6장을 채우기 전이라도 먼저 run이나 triplet이 되는 사람이 승자가 된다.

두 사람이 가져가게 되는 순서대로 12장의 카드에 대한 정보가 주어졌을 때 승자를 알아내는 프로그램을 작성하시오. 만약 무승부인 경우 0을 출력한다.

예를 들어 9 9 5 6 5 6 1 1 4 2 2 1인 경우, 플레이어 1은 9, 5, 5, 1, 4, 2카드를, 플레이어2는 9, 6, 6, 1, 2, 1을 가져가게 된다.

이때는 카드를 모두 가져갈 때 까지 run이나 triplet이 없으므로 무승부가 된다.

#### 풀이

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

  