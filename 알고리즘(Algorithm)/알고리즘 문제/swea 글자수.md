# swea

# 글자수

### 일자 20200825

#### 풀이 1

```python
'''
3
XYPV
EOGGXYPVSY
STJJ
HOFSTJPVPP
ZYJZXZTIBSDG
TTXGZYJZXZTIBSDGWQLW
'''

def brute(s1, s2):
    i, j = 0, 0
    while i < len(s1) and j < len(s2):
        if s1[i] != s2[j]:
            j = j-i
            i = -1
        i += 1
        j += 1
    if i == len(s1):
        return 1
    else:
        return 0

for tc in range(1,int(input())+1):
    str1 = input()
    str2 = input()
    # print(str1, str2)

    #계산
    result = brute(str1, str2)
    print('#{} {}'.format(tc, result))
```



### 풀이 2

```python
T = int(input())
for tc in range(1,T+1):
    str1 = input()
    str2 = input()
    # 딕셔너리 사용
    count = {}.fromkeys(str1,0)
    # print(count)
    for ch in str2:
        if ch in count:
            count[ch] += 1
    # print(count)
    print("#{} {}".format(tc, max(count.values())))
```

- 주어진 두개의 문자열을 비교해 두번째 문자열 속에서 해당되는 첫번째 문자열의 최대의 길이를 구하는 문제이다. 
- brute 문제 중 하나이며, 존재유무 보다 한발 더 나아가 두 문자열을 비교하며 카운팅 해나가야 하는 응용문제이다.
- 꽤 기초문제인 편이라 어렵지는 않았다.
- 이후에는 딕셔너리를 활용해 푸는 방법도 익혀보아, 총 두가지 방식으로 문제를 풀어보았다.

