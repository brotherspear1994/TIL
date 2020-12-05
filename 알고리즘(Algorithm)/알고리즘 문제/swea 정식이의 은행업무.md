# swea

# 정식이의 은행업무

### 일자 20201029

#### 문제

삼성은행의 신입사원 정식이는 실수를 저질렀다.

은행 업무가 마감되기 직전인 지금, 송금할 금액을 까먹고 말았다.

하지만 다행스럽게도 정식이는 평소 금액을 2진수와 3진수의 두 가지 형태로 기억하고 다니며, 기억이 명확하지 않은 지금조차 2진수와 3진수 각각의 수에서 단 한 자리만을 잘못 기억하고 있다는 것만은 알고 있다. 

예를 들어 현재 기억이 2진수 1010과 3진수 212을 말해주고 있다면 이는 14의 2진수인 1110와 14의 3진수인 112를 잘못 기억한 것이라고 추측할 수 있다.

정식이는 실수를 바로잡기 위해 당신에게 부탁을 하였다.

정식이가 송금액을 추측하는 프로그램을 만들어주자.

( 단, 2진수와 3진수의 값은 무조건 1자리씩 틀리다.  추측할 수 없는 경우는 주어지지 않는다. )

![img](https://swexpertacademy.com/main/common/fileDownload.do?downloadType=CKEditorImages&fileId=AWMeZPm6k5MDFAXd)


**[입력]**

10개 이하의 테스트 케이스가 주어진다.

첫 번째 줄에는 테스트케이스의 개수가 주어진다.

하나의 케이스는 두 줄로 되어있다.

각 케이스의 첫 번째 줄은 정식이가 기억하는 송금액의 2진수 표현, 두 번째 줄은 송금액의 3진수 표현이 주어진다.  

(3 ≤ 2진수, 3진수의 자릿수 <40)

#### 풀이 1

```python
def binary(k, bi):
    if k == len(bi):
        return
    temp = bi[:]
    bi[k] = 1
    if temp == bi:
        binary(k+1, bi)
    else:
        bi_stack.append(bi[:])
 
 
    bi[k] = 0
    if temp == bi:
        binary(k+1, bi)
    else:
        bi_stack.append(bi[:])
        bi[k] = 1
 
 
def triple(k, tri):
    if k == len(tri):
        return
 
    temp = tri[:]
 
    tri[k] = 0
    if temp == tri:
        triple(k+1, tri)
    else:
        tri_stack.append(tri[:])
    tri[k] = 1
    if temp == tri:
        triple(k+1, tri)
    else:
        tri_stack.append(tri[:])
    tri[k] = 2
    if temp == tri:
        triple(k+1, tri)
    else:
        tri_stack.append(tri[:])
        tri[k] = temp[k]
 
T = int(input())
for tc in range(1,T+1):
    bi = list(map(int, input()))
    tri = list(map(int, input()))
    # print(bi, tri)
    temp_bi = bi[:]
    temp_tri = tri[:]
    bi_stack = []
    tri_stack = []
 
 
    binary(0, temp_bi)
    triple(0, temp_tri)
    # print(bi_stack, tri_stack)
    bi_value = set()
    tri_value = set()
 
    for i in range(len(bi_stack)):
        temp = 0
        for j in range(len(bi_stack[i])):
            temp += bi_stack[i][j]*(2**(len(bi_stack[i])-j-1))
        bi_value.add(temp)
 
    for i in range(len(tri_stack)):
        temp = 0
        for j in range(len(tri_stack[i])):
            temp += tri_stack[i][j]*(3**(len(tri_stack[i])-j-1))
        tri_value.add(temp)
 
 
    for element in bi_value:
        if element in tri_value:
            ans = element; break
    print("#{} {}".format(tc, ans))
```



#### 풀이 2

```python
for tc in range(1,int(input())+1):
    bianry = input()
    triplet = input()
    dlist = []
    # 이진수
    for i in range(len(bianry)):
        digit = 0
        for j in range(len(bianry)):
            if i == j:
                c = '1' if bianry[j] == '0' else '0'
                digit = digit*2 + int(c,2)
            else:
                c = bianry[j]
                digit = digit*2 + int(c,2)
        dlist.append(digit)
    # 삼진수
    for i in range(len(triplet)):
        for j in range(len(triplet)):
            t1 = list(triplet)
            if i == j:
                for k in ['0','1','2']:
                    if t1[j] != k:
                        t1[j] = k
                        digit = 0
                        for m in range(len(t1)):
                            c = t1[m]
                            digit = digit*3+int(c,3)
                        if digit in dlist:
                            ans = digit
    print("#%d" % tc, ans)
```

- 내 풀이 방식과 교수님의 풀이 방식, 두가지 방식으로 풀어봤다.
- 우선 각 자리의 수를 한번씩 표현할 수 있는 모든 가지수로 만든 후 이진수의 값과 삼진수의 값이 일치하는지 여부를 체크하는 포인트는 동일하다.
- 항상 하나의 문제도 여러 가지 방법의 풀이법을 학습하고 나혼자 코드를 보지않고 풀어보는 습관을 들이려 노력중이다.