# swea

# 반복문자 지우기

### 일자 20200827

### 문제

문자열 s에서 반복된 문자를 지우려고 한다. 지워진 부분은 다시 앞뒤를 연결하는데, 만약 연결에 의해 또 반복문자가 생기면 이부분을 다시 지운다.

반복문자를 지운 후 남은 문자열의 길이를 출력 하시오. 남은 문자열이 없으면 0을 출력한다.


다음은 CAAABBA에서 반복문자를 지우는 경우의 예이다.


C**AA**ABBA 연속 문자 AA를 지우고 C와 A를 잇는다.

CA**BB**A 연속 문자 BB를 지우고 A와 A를 잇는다.

C**AA** 연속 문자 AA를 지운다.

C 1글자가 남았으므로 1을 리턴한다.

 


**[입력]**


첫 줄에 테스트 케이스 개수 T가 주어진다. 1≤T≤ 50


다음 줄부터 테스트 케이스의 별로 길이가 1000이내인 문자열이 주어진다.

 

**[출력]**


\#과 1번부터인 테스트케이스 번호, 빈칸에 이어 답을 출력한다.

#### 풀이1

```python
for tc in range(1,int(input())+1):
    s = list(input())
    # print(s)
    # s.pop(0)
    # print(s)

    i = 0
    while len(s) >= 2 and i < len(s)-1:
        stack = []
        if s[i] == s[i+1]:
            stack.extend(s[i:i+2])
            # print(stack)
            for _ in range(len(stack)):
                s.pop(i)
            stack = []
            i = -1
        i += 1
    # print(s)
    print("#{} {}".format(tc, len(s)))
```

- while문과 stack을 활용해 주어진 문자열에서 반복되는 문자열을 순차적으로 제거해주는 작업을 해주면 된다.



### 풀이 2

```python
for tc in range(1, int(input())+1):
    arr = input()
    S = []

    for ch in arr:
        if not S:
            S.append(ch) # 빈스택인 경우
        elif ch != S[-1]: # ch와 S[-1] 비교해서 다르면 push
            S.append(ch)
        else:
            S.pop()
    print(len(S))
```

- 위와 비슷하지만 다소 차이가 있는 풀이법도 추후 익혔기 때문에, git에 추가해둔다.