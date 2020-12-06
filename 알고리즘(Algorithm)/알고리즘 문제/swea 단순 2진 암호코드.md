# swea

# 단순 2진 암호코드

### 일자 20201027

#### 문제

[본문 링크 참고하기](https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AV15FZuqAL4CFAYD&categoryId=AV15FZuqAL4CFAYD&categoryType=CODE)

#### 풀이

```python
pwd = ['0001101','0011001','0010011','0111101','0100011',
       '0110001','0101111','0111011','0110111','0001011']

def getCode():
    global code
    for i in range(N):
        for j in range(M-1,-1,-1):
            if arr[i][j] == '1':
                start = j-55
                for k in range(56):
                    code[k] = arr[i][start]
                    start += 1
                return

def codeCal(digit_code):
    a = digit_code[0] + digit_code[2] + digit_code[4] + digit_code[6]
    b = digit_code[1] + digit_code[3] + digit_code[5] + digit_code[7]
    if (a*3+b) % 10 == 0:
        return a+b
    else:
        return 0

for tc in range(1, int(input())+1):
    N, M = map(int, input().split())
    arr = [list(input()) for _ in range(N)]
    # for row in arr:
    #     print(row)
    code = [0]*56
    digit_code = [0]*8

    getCode()
    # print(code)

    str = ""
    dist = 0
    for i in range(len(code)):
        idx = i % 7
        str += code[i]
        if idx == 6:
            digit_code[dist] = pwd.index(str)
            str = ""
            dist += 1
    # print(digit_code)

    ans = codeCal(digit_code)
    print("#%d" % tc, ans)



# def getCode():  #2차원 배열에서 코드 얻기
#     global code
#     for i in range(N):
#         for j in range(M-1,-1,-1):
#             if arr[i][j] == '1':    #뒤에서 부터 읽어서 1을 발견
#                 idx = j - 55
#                 for k in range(56):
#                     code[k] = arr[i][idx]
#                     idx +=1
#                 return
#
# def checkCode():    #정상적인 코드인지 검사
#     a = digitCode[0] + digitCode[2] +digitCode[4] + digitCode[6]
#     b = digitCode[1] + digitCode[3] + digitCode[5] + digitCode[7]
#     # print(a,b)
#     if (a*3 + b) % 10 ==0 : #코드 검증 잘됨
#         return a+b
#     else:   #코드검증 실패
#         return 0
#
# #암호코드
# pwd = ['0001101','0011001','0010011','0111101','0100011',
#        '0110001','0101111','0111011','0110111','0001011']
# T = int(input())
# for tc in range(1,T+1):
#     N,M = map(int,input().split())
#     arr = [list(input()) for _ in range(N)]
#     # print(arr)
#     code =[0] * 56  #암호코드 저장
#     digitCode = [0]* 8  #변환코드 저장
#     getCode()
#     # print(code)   #암호코드 찾아냄
#     str = ""
#     dist = 0
#     for i in range(len(code)):  #암호코드를 순회하면서
#         idx = i % 7
#         str += code[i]  #0과 1로 이뤄진 문자열 코드 생성
#         if idx == 6:
#             # print(str)
#             digitCode[dist] = pwd.index(str)
#             str =""
#             dist +=1
#     # print(digitCode)
#     cnt = checkCode()
#     print("#{} {}".format(tc, cnt))
```

