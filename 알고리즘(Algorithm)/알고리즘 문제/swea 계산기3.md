# swea

# 계산기 3

### 일자 20200901



### 문제

문자열로 이루어진 계산식이 주어질 때, 이 계산식을 후위 표기식으로 바꾸어 계산하는 프로그램을 작성하시오.

예를 들어

“3+(4+5)*6+7”

라는 문자열로 된 계산식을 후위 표기식으로 바꾸면 다음과 같다.

"345+6*+7+"

변환된 식을 계산하면 64를 얻을 수 있다.

문자열 계산식을 구성하는 연산자는 +, * 두 종류이며 문자열 중간에 괄호가 들어갈 수 있다.

이 때 괄호의 유효성 여부는 항상 옳은 경우만 주어진다.

피연산자인 숫자는 0 ~ 9의 정수만 주어진다.

**[입력]**

각 테스트 케이스의 첫 번째 줄에는 테스트 케이스의 길이가 주어진다. 그 다음 줄에 바로 테스트 케이스가 주어진다.

총 10개의 테스트 케이스가 주어진다.

**[출력]**

\#부호와 함께 테스트 케이스의 번호를 출력하고, 공백 문자 후 답을 출력한다.

#### 풀이1

```python
for tc in range(1, 11):
    N = int(input())
    Data = input()
    new_data = ''
    # print(Data)
    stack_data = []
    num_list = ['0','1','2','3','4','5','6','7','8','9']
    op_lst = ["+", "-", "*", "/"]

    for element in Data:
        # print(type(element))
        if element in num_list: new_data += element
        elif element == '(':
            stack_data.append(element)
        elif element == ')':
            while True:
                if stack_data[-1] == '(': break
                new_data += stack_data.pop()
            stack_data.pop()
        elif element in op_lst:
            if len(stack_data) == 0:
                stack_data.append(element)
            elif element == '+':
                while len(stack_data) > 0:
                    if stack_data[-1] == '(': break
                    new_data += stack_data.pop()
                stack_data.append(element)
            elif element == '-':
                while len(stack_data) > 0:
                    if stack_data[-1] == '(': break
                    new_data += stack_data.pop()
                stack_data.append(element)
            elif element == '*':
                while len(stack_data) > 0:
                    if stack_data[-1] != '/' and stack_data[-1] != '*': break
                    new_data += stack_data.pop()
                stack_data.append(element)
            elif element == '/':
                while len(stack_data) > 0:
                    if stack_data[-1] != '/' and stack_data[-1] != '*': break
                    new_data += stack_data.pop()
                stack_data.append(element)
    while len(stack_data) > 0:
        new_data += stack_data.pop()
    # print(new_data)

    stack = []
    for element in new_data:
        if element in num_list: stack.append(element)
        elif element in op_lst:
            num2, num1 = stack.pop(), stack.pop()
            if element == "+": result = int(num1) + int(num2); stack.append(result)
            elif element == "-": result = int(num1) - int(num2); stack.append(result)
            elif element == "*": result = int(num1) * int(num2); stack.append(result)
            elif element == "/": result = int(num1) // int(num2); stack.append(result)
    print("#{} {}".format(tc, int(stack[0])))
```

- 이 문제도 마찬가지로 `후위표기식`에 대한 개념을 어느정도 알고 있는 상태에서 풀어야만 한다.
- 코드상으로는 길이가 길어 문제가 어려워 보이지만, 입력값을 받고 우선 후위표기식으로 다시 정리해 준다.
- 이후 후위표기식으로 정리된 데이터를 스택을 활용해 다시 차근차근 계산해주면 된다.



#### 풀이2

```python
T = 10
operator = ['+', '*']
braket = ["(", ")"]

def isNumber(x):  # 숫자인지 아닌지 판단
    if x not in operator and x not in braket:
        return True
    else:
        return False


def isp(token):  # 토큰의 우선순위 리턴 => 스택안의 토큰의 우선순위
    if token == "*" or token == "/":
        return 2
    elif token == "+" or token == "-":
        return 1
    elif token == "(":
        return 0


def icp(token):  # 스택안으로 들어오는 토큰의 우선순위
    if token == "*" or token == "/":
        return 2
    elif token == "+" or token == "-":
        return 1
    elif token == "(":
        return 3


for tc in range(1, T + 1):
    N = int(input())
    infix = list(input())
    # print(infix)
    postfix = []
    stack = []
    for c in infix:
        if isNumber(c):  # 숫자면
            postfix.append(c)
        elif c == ")":  # 닫는 괄호면 -> 여는괄호 만날때까지 팝
            while len(stack) > 0:  # 스택이 비어있지 않는 동안
                top = stack.pop()
                if top == "(":  # 여는 괄호 만나면 끝! (버림)
                    break
                postfix.append(top)
        else:  # 나머지 연산자면(닫는 괄호가 아닌 연산자)
            if len(stack) == 0:  # 스택이 비어있으면 스택에 그냥 넣기
                stack.append(c)
            else:  # 아니면 우선순위 비교
                while len(stack) > 0:  # 스택이 빌때까지 반복
                    top = stack[-1]  # 스택의 가장 위의 원소
                    if icp(c) > isp(top):  # 토큰의 우선순위가 스택의 top의 우선순위 보다 크면
                        stack.append(c)  # 스택에 넣음
                        break
                    postfix.append(stack.pop())
    while stack:
        postfix.append(stack.pop())
    # print(postfix)
    # 후위 표기법을 계산 (스택을 이용해서)
    stack = []
    for c in postfix:
        if c not in operator:  # 숫자면
            stack.append(int(c))
        else:
            op1 = stack.pop()
            op2 = stack.pop()
            if c == "+":
                stack.append(op2 + op1)
            elif c == "*":
                stack.append(op2 * op1)
    result = stack.pop()
    print("#{} {}".format(tc, result))
```

- 내가 직접 문제를 푼 후, 교수님의 풀이법도 익혔다. 코드에 대한 설명은 주석을 통해 간략하게 나마 남겨놓았다.
- 교수님 풀이 시간 후에는 코드를 이해하는 시간을 갖고, 안보고 혼자 코드를 짜보는 시간도 가졌다.