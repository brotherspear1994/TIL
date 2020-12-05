# swea

# 단어공부

### 일자 20200825

#### 풀이

```python
'''
Mississipi
'''

Str = input()
count = [0 for _ in range(26)]

print(ord("Z"))
print(ord("a"))
print(ord("A"))
for ch in Str:
    if ord(ch) <= 90:   # 대문자
        n= ord(ch) - ord("A")
    elif ord(ch) >= 97: #소문자
        n = ord(ch) - ord("a")      
    count[n] += 1
# print(count)
max = 0
maxidx = 0
for i in range(len(count)):
    if max < count[i]:
        max = count[i]
        maxidx = i
cnt_max = 0
print(max)
for c in count:
    if c == max:
        cnt_max += 1
ans = ""
if cnt_max > 1:
    ans = "?"
else:
    ans = chr(maxidx+65)
print(ans)
```

- 단어를 for문으로 순회하며 각 알파벳의 대소문자 구분과 문자열을 아스키코드 기준으로 숫자로 치환했을 때 몇인지를 구한다.
- 또한 각 알파벳(대소문자 구분)이 몇개 나왔는지도 구하는 문제이다.
- 직접 알파벳을 아스키코드 치환 명령어(ord)로 찍어보며 풀어보면 된다.
- 개념을 익힌 후에는 혼자서 풀어보는 과정도 당연히 해보았다.
