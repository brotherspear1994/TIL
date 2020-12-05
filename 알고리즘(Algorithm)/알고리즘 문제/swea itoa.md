# swea

# itoa 연습문제

### 일자 20200825

#### 풀이

```python
def itoa(num):
    x = num
    y = 0
    arr = []
    while x:
        y = x % 10
        x = x // 10
        arr.append(chr(y + ord('0')))

    arr.reverse()
    str = "".join(arr)
    return str


x = 123
print(x, type(x))
str = itoa(x)
print(str, type(str))
```

- int 타입의 숫자가 주어지면 이를 똑같은 모양의 문자열로 바꾸는 연습을 했다.
- 앞서 연습했던 atoi 알고리즘의 반대 버전으로, 직접 str기능을 구현해 본거라 할 수 있다.

```python
str1 = "abc 1,2 ABC"
print(str1)
str1 = str1.replace("1,2", "one, two")
print(str1)
```

- 추가로 replace 라이브러리의 기능도 알아보았다.