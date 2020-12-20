# swea

# 특이한 자석

### 일자 20201020

### 문제

[본문참조 링크](https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AWIeV9sKkcoDFAVH&categoryId=AWIeV9sKkcoDFAVH&categoryType=CODE)

### 풀이1

```python
for tc in range(1, int(input())+1):
    K = int(input())
    mag = [list(map(int, input().split())) for _ in range(4)]
    for _ in range(K):
        idx, spin = map(int, input().split())
        idx -= 1
        move = [(idx, spin)]


        # 왼쪽 톱니
        temp = spin
        for i in range(idx-1,-1,-1):
            if mag[i][2] != mag[i+1][6]:
                temp *= -1
                move.append((i, temp))
            else:
                break

        # 오른쪽 톱니
        temp = spin
        for i in range(idx+1,4):
            if mag[i-1][2] != mag[i][6]:
                temp *= -1
                move.append((i, temp))
            else:
                break
        # 회전
        for idx, spin in move:
            if spin == 1:
                mag[idx] = [mag[idx].pop()] + mag[idx]
            elif spin == -1:
                mag[idx].append(mag[idx].pop(0))
    ans = 0
    for i in range(4):
        ans += mag[i][0]* 2**i
    print("#%d" % tc, ans)
```



### 풀이2

```python
T = int(input())
for tc in range(1,T+1):
    K = int(input()) # 회전 횟수
    magnet = [list(map(int,input().split())) for _ in range(4)]
    for _ in range(K): # K번반복
        idx, rot = map(int, input().split())
        idx -= 1 #0번 부터 시작하도록 조정
        r = [0,0,0,0] # 각 자석의 회전정보 저장
        r[idx] = rot #회전할 자석의 방향 저장
        tmp = rot
        # 왼쪽 방향 회전 여부확인
        for i in range(idx-1, -1, -1):
            if magnet[i][2] != magnet[i+1][6]:
                tmp *= -1
                r[i] = tmp
            else:
                break
        # 오른쪽 방향 회전 여부확인
        tmp = rot
        for i in range(idx+1,4):
            if magnet[i][6] != magnet[i-1][2]:
                tmp *= -1
                r[i] = tmp
            else:
                break
        print(tc, r)
        #회원정보를 가지고 회전시키기
        for j in range(4):
            if r[j] != 0:
                rotate(j, r[j])
    result = 0
    for i in range(4):
        result += magnet[i][0] * (2**i)

    print("#{} {}".format(tc, result))
```



### 풀이3

```python
def rotate(N, D):
    if D == 1:
        temp = magnet[N][7]
        for i in range(6,-1,-1):
            magnet[N][i+1] = magnet[N][i]
        magnet[N][0] = temp
    else:
        temp = magnet[N][0]
        for i in range(1,8):
            magnet[N][i-1] = magnet[N][i]
        magnet[N][7] = temp

for tc in range(1,int(input())+1):
    K = int(input())
    magnet = [list(map(int,input().split())) for _ in range(4)]
    for _ in range(K):
        n, d = map(int,input().split())
        n -= 1
        move = [(n,d)]

        # 왼쪽 회전
        temp = d
        for i in range(n-1,-1,-1):
            if magnet[i][2] != magnet[i+1][6]:
                temp *= -1
                move.append((i, temp))
            else:
                break
        # 오른쪽 회전
        temp = d
        for i in range(n+1,4):
            if magnet[i-1][2] != magnet[i][6]:
                temp *= -1
                move.append((i,temp))
            else:
                break

        # 회전시키기
        for i in range(len(move)):
            rotate(move[i][0],move[i][1])
    ans = 0
    for i in range(4):
        ans += magnet[i][0]*(2**i)
    print("#{} {}".format(tc, ans))
```

- 처음으로 정식 시뮬레이션 문제를 풀었던 때이다.
- 지금도 그렇지만 당시에는 시뮬레이션 유형을 처음 푸는거라, 나 혼자 푸는데 굉장히 애를 먹었다.
- 문제에서 주어진 대로 톱니를 돌리는 알고리즘을 구현하기란 쉽지 않았다.
- 시뮬레이션은 기타 기본 알고리즘 유형처럼, 문제를 푸는 법이나 공식이 정형화 돼있지 않고, 통합적인 알고리즘들을 이용해 문제마다 다르게 문제에서 주어진대로 시뮬레이션을 구현하는 거라 매우 어려운 것 같다.