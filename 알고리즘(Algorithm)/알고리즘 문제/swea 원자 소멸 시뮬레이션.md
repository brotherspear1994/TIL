# swea

# 원자 소멸 시뮬레이션

### 일자 20201203

### 문제

[본문 링크 참조](https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AWXRFInKex8DFAUo&categoryId=AWXRFInKex8DFAUo&categoryType=CODE)

#### 풀이1(시간 초과 발생코드)

```python
import copy; from collections import deque

dx = [0,0,-1,1]
dy = [1,-1,0,0]

for tc in range(1,int(input())+1):
    N = int(input())
    atoms = deque()

    for _ in range(N):
        x,y,dir,k=map(int, input().split())
        atoms.append([x*2,y*2,dir,k])

    ans = 0
    for _ in range(4000):
        temp = copy.deepcopy(atoms)
        if len(temp) <= 1: break
        dict = {}
        for _ in range(len(temp)):
            x, y, dir, k = atoms.popleft()
            x, y, dir, k = x+dx[dir], y+dy[dir], dir, k
            if min(x,y) < -2000 or max(x,y) > 2000:
                continue
            try: dict[(x,y)].append([x,y,dir,k])
            except: dict[(x,y)] = [[x,y,dir,k]]

        for key in dict:
            dic = dict[key]
            if len(dic) > 1:
                for atom in dic:
                    ans += atom[3]
            else:
                atoms.append(dic[0])
    print("#%d" %tc, ans)
```

- 런타임 에러가 발생해 코드를 처음부터 갈아엎고 아예 다른방법으로 풀어보았다.

#### 풀이2

````python
import sys; sys.stdin = open('원자력.txt', 'r')

dx = [0,0,-1,1] # dir 값에 따라 원자의 좌표를 이동시켜줄 dx, dy 설정
dy = [1,-1,0,0]

for tc in range(1,int(input())+1):
    N = int(input())
    atoms = []

    for _ in range(N):
        x,y,d,k = map(int, input().split())
        atoms.append([2*x,2*y,d,k])
        # 이동중 만나는 케이스(0.5 이동)를 처리해 주기 위해 각 좌표에 2를 곱해 모두 짝수로 만들어줘 무조건 좌표위에서 만나게 해준다.

    ans = 0
    while atoms: # 폭파 이전에 범위를 벗어나도 원자가 소멸되므로 원자가 존재할때까지 while문 반복
        temp, set1, set2 = [], set(), set()
        for atom in atoms: # 원자정보가 담긴 배열을 돌며
            atom[0] += dx[atom[2]]; atom[1] += dy[atom[2]] # 이동 시켜주고
            check_len = len(set1) # set의 길이를 기록
            set1.add((atom[0], atom[1])) # 담아주고
            if check_len == len(set1): set2.add((atom[0],atom[1]))
            # 만일 set의 길이가 변동이 없다면 이미 set에 해당 좌표가 존재한다는 의미이고, 이는 원자끼리 충돌했다는 의미이므로
            # 소멸될 원자를 담아두는 set2에 담아준다.
        for x,y,d,k in atoms: # 소멸될 다른 원자를 찾아줄거임.
            if (x,y) in set2: ans += k # 소멸될 원자는 전부 에너지 값으러 전환
            elif min(x,y) < -2000 or max(x,y) > 2000: continue 
            # 범위를 벗어난 원자도 제외(2배 시켜줬으니 문제에서 준 범위보다 2배 범위로 잡아준다,)
            else: temp.append([x,y,d,k])
            # 소멸되지 않았거나 범위안의 원자를 temp에 저장
        atoms = temp # atoms를 temp로 최신화
    print("#%d %d"%(tc, ans))
````

- 문제풀기 성공!
- 이때부터는 슬슬 시뮬레이션 유형의 문제들을 푸는 연습을 가졌다.

