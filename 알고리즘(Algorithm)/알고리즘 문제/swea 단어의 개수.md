# swea

# 단어의 개수 연습문제

### 일자 20200825

#### 풀이

```python
'''
 Mazatneunde Wae Teullyeoyo
'''
str = input()
# print(str)
cnt = 0
words = False

for ch in str:
    if ch == ' ':
        if words:
            cnt += 1
            words = False
    else:
        words = True
if words:
    cnt += 1

print(cnt)

# 풀이 2
arr = list(input())

i_index = 0
cnt=0
for i in arr:
    i_index += 1
    if i == ' ' and len(arr) == 1:
        print(0)
    else:
        if i == ' ' and i_index != len(arr) and i_index != 1:
            cnt +=1

if not (' ' in arr and len(arr)) == 1:
    print(cnt+1)
    
    
# 풀이 3
def removeAll(l, i):
    try:
        while True: l.remove(i)
    except ValueError:
        pass

Alpha = input()
ord_lst = []
for i in Alpha:
    ord_lst.append(ord(i))

cnt_sub = 0
cnt_max = 0
alpha_ord = 0
overlap = True
for j in range(0, len(ord_lst)):
    for k in ord_lst:
       if ord_lst[j] == k:
           cnt_sub += 1
    if cnt_sub > cnt_max:
        cnt_max = cnt_sub
        alpha_ord = ord_lst[j]
        removeAll(ord_lst, alpha_ord)
    elif cnt_sub == cnt_max:
        overlap = False
        print('?')
        break
    cnt_sub = 0

if overlap:
    print((chr(alpha_ord)).upper())
    
# 풀이 4
T = input().upper()
t = []
for i in set(T):
    # print(set(T))
    t.append(T.count(i))
    # print(t)

idx = [a for a, b in enumerate(t) if t[a]==max(t)]
if len(idx) >= 2: print('?')
else: print(list(set(T))[t.index(max(t))])
```

- 띄어쓰기를 기준으로 문장 속에 단어의 개수가 몇개가 들어있는지 판단하는 기본적인 문제이다.

- 비슷한 유형의 문제를 여러 풀이 방법으로 풀어보았다.
- 워낙 기본적인 문제이지만 for문을 돌리면서 각 요소를 어떻게 처리하는지에 대한 매우 기초적인 훈련이기 때문에 여러가지 풀이방법으로 반복 숙달하는 연습을 했다.