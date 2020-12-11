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

#### 풀이

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