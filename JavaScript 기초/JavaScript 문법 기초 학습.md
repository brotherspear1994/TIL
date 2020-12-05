# ECMAScript

[toc]

## 1.변수와 식별자

### 01.1 식별자

>  변수명은 식별자라고 불리며 특정 규칙을 따라야 한다. 

- 반드시 문자, 달러, _로 시작해야 한다. 숫자로 시작할 수 없다.(`-`도 안됩니다.)
- 대소문자를 구분합니다. 클래스명이 아니라면 시작 단어는 대문자 사용을 지양해야한다.
- 예약어도 사용 불가능 하다.(class, const, let, var, await, case...)

#### 식별자 작성 스타일

- 기본적으로 camelCase로 작성합니다. (lowcaseUppercase)

  ```javascript
  // 숫자, 문자, 불린
  let dog
  let babyCat
  
  // 배열 - 배열ㅇ느 복수형으로 작성합니다.
  let animals
  
  // 함수
  function getPropertyName() {}
  
  // 이벤트 핸들러 - 이벤트 핸들러는 'on'으로 시작한다.
  function onClick () {}
  function onKeyDown () {}
  
  // 불린 반환 함수 - 리턴 값이 true, false - 'is'로 시작한다.
  function isAuthenticated() {}
  ```

- PascalCase로 작성되는 경우 - 클래스, 생성자

  ```javascript
  class User {
      information(option) {
          this.name = option.name
      }
  }
  
  const people = new User({
      name = '홍길동',
  })
  ```

- 대문자 스네이크 케이스(SNAKE_CASE)

- 값이 변하지 않는다는 것을 알립니다.

  ```javascript
  const API_KEY = 'api_key'
  const PI = '3.14.....'
  ```

  

### 01.2 변수

#### let(변수): 값을 재할당 할 수 있는 변수를 선언하는 키워드

 ```javascript
let x = 1
x = 3
 ```

- 선언은 단 한번만 가능하다.

```javascript
let x = 3
let x = 2
```

- 유효 범위가 블록을 기준으로 작성이 된다.
- 블록 유효 범위란 -> `if`, `for` 등등 {} 내부를 가리킨다.

```javascript
let x = 1

if (x===1) {
    let x = 2
    cosole.log(x)
}
cosole.log(x)
```

​	

#### const(상수):  재 할당도 재 선언도 불가능하다.

- 값이 변하지 않는 상수를 선언하는 키워드

  ``` javascript
  const x = 4
  x = 3 
  console.log(x)
  
  // 4 나옴.
  
  const foo = {}
  foo.bar = 4
  console.log(foo)
  console.log(foo.bar)
  
  // object를 어딘가에 할당하면, 이 친구의 주소값이 할당되기 때문에 위가 가능.
  ```

- const는 상수 선언 시 반드시 값을 초기화해 줘야 한다.

  ```javascript
  // 불가능
  const a
  
  // 반드시 값을 초기화 해줘야 한다.
  const a = 3
  ```

- let과 같이 블록 유효범위를 가집니다.

  ```javascript
  const num = 3
  
  if (num === 3) {
      const num = 4
      console.log(num)
  }
  console.log(num)
  ```

#### var(변수): ES6 이전에 사용하던 변수 선언 방식

- 재할당도 가능하고 재선언도 가능.

- 예기치 못한 상황을 발생 시킬 수 있으므로 `절대 사용하지 않는것을 권장한다.`

  ```javascript
  var x = 3
  var x = 2
  cosole.log(x)
  ```

  - var는 함수 유효 범위를 가짐.

    ```javascript
    var x = 33
    let y = 11
    if (x == 33) {
        var x = 22
        let y = 1
        console.log(x) // 22
        console.log(y) // 1
    } 
    console.log(x) // 22
    console.log(y) // 11
    ```

#### 정리

| const       | let         | var            |
| ----------- | ----------- | -------------- |
| 재할당 불가 | 재할당 가능 | 재할당 가능    |
| 재선언 불가 | 재선언 불가 | 재선언 가능    |
| block scope | block scope | function scope |

### 01.3 Hoisting

- `var`로 선언한 변수가 선언 이전에 참조 될 수 있는 현상.

- hoisting은 우리가 활용하는 기술 X, 피해야 하는 상황임.

  ```javascript
  console.log(name)
  
  var name = '홍길동'
  ```

  - 자바스크립트 코드 실행하면 다음과 같이 이해한다.

    ```javascript
    var name
    console.log(name)
    
    var name = '홍길동'
    ```

- let으로 작성 했을 시

  ```javascript
  console.log(name)
  
  let name = '홍길동'
  // const name = '홍길동'
  ```

  

## 02. 타입과 연산자

### 02.1 Primitive(원시값, 원시 자료형) 자료형 타입

#### Number

```javascript
const a = 1
const b = -13
const c = 3.14
const d = 2.99e3
const e = Infinity
const f = -Infinity
const g = NaN

console.log(a, b, c, d, e, f, g)
```

 #### String

```javascript
const sentence1 = '문자열'
const sentence2 = "문자열"

console.log(sentence1)
console.log(sentence2)
```

- 문자열 간의 덧셈의 가능하다

  ```javascript
  const firstName = '구현'
  const lastName = '김'
  
  const fullName = firstName + lastName
  console.log(fullName)
  
  // 구현김
  ```

- escape sequence

  ```javascript
  const hello = "안녕 \n 하세요"
  
  console.log(hello)
  ```

- Template literals

  ```javascript
  const name = '홍길동'
  
  const sayHello = `${name}이 인사합니다.`
  console.log(sayHello)
  ```

- 템플릿 리터럴은 escape sequence를 사용 할 수 없다. 

  ```javascript
  const nextSentence = `안녕
  하세요`
  // 그냥 밑으로 내리면 됨.
  console.log(nextSentence)
  ```



#### Boolean

```javascript
true
false
```



#### Empty Value

- 값이 존재하지 않음을 나타내는 방식은 2가지가 있다.

- undefined - 값을 할당하지 않았을 때 JS가 자동으로 할당 해주는 값

  ```javascript
  let name
  console.log(name)
  ```

- null - 값이 없음을 나타내기 위해 사용한다.

  ```javascript
  let name = null
  console.log(name) 
  ```

  ```javascript
  typeof null
  "object"
  
  typeof undefined
  "undefined"
  ```



### 02.2 연산자

#### 할당 연산자

- 연산과 동시에 변수에 어떠한 값을 할당하는연산자

  ```javascript
  let c = 10
  c += 10
  console.log(c)
  
  c -= 10
  console.log(c)
  
  c *= 10
  console.log(c)
  
  c /= 10
  console.log(c)
  
  c++
  console.log(c) // 증강식 1을 더해주는 역할
  
  c--
  console.log(c) // 증강식 1을 빼주는 역할
  ```

  

#### 비교 연산자

- 두 값을 비교하기 위해 사용하며, `true` or `false`를 반환한다.

  ```javascript
  3 > 2 // true
  3 < 2 // false
  ```

- 문자열도 비교가 가능. 영어 소문자가 대문자보다 큰 값을 가진다.

- 알파벳은 오름차순으로 비교한다.

  ```javascript
  'A' < 'a'
  ```

#### 동등 연산자(==)

- 형변환 했을 때 같은 값이면 일치한다고 본다.
- JS는 자동으로 형 변환을 해준다.
- 자동 형변환으로 인한 예기치 못한 상황이 발생할 수 있다. 그러므로 `동등 연산자 사용은 지양해야한다`.

```javascript
const a = 1
const b = '1'

console.log(a == b)
console.log(a == Number(b)) // `==`는 자동으로 형변환 해줌.
```



#### 일치 연산자(===)

- 동등 연산자보다 엄격한 비교를 합니다.

  ```javascript
  const a = 1
  const b = '1'
  
  console.log(a === b) // false
  console.log(a === Number(b)) // true
  ```

#### 논리 연산자

- `and` &&

  ```javascript
  true && true // true
  true && false // false
  
  0 && 0 // 0
  1 && 0 // 0
  4 && 7 // 7 (단축 평가, 4도 트루 7도 트루, 맨 나중 트루값을 반환(비교 끝난시점))
  ```

- `or` ||

  ```javascript
  true || false
  false || false
  
  1 || 0 // 1
  4 || 7 // 4
  ```

- `not` !

  ```javascript
  !true // false
  ```

#### 삼항 연산자

- 가장 앞의 조건식이 참이면 `:`을 기준으로 작성한 앞의 값이 반환되고, 반대의 경우 `:` 뒤의 값이 반환된다.

  ```javascript
  true ? 1 : 2 // 1
  false ? 1:2 // 2
  ```

  ```javascript
  const result = 3.14 > 4 ? 'Yes' : 'No'
  console.log(result)
  ```

  

## 3. 조건문과 반복문

### 03.1 조건문

#### `if`, `else if`, `else`

- if

  ```javascript
  const name = 'kim'
  	
  if (name === 'kim') {
      console.log('True')
  }
  ```

- else if

  ```javascript
  const name = 'park'
  
  if (name === 'lee') {
      console.log('LEE')
  } else if (name === 'kim') {
      console.log('KIM')
  } else {
      console.log(`${name}`)
  }
  ```



#### switch

- 하나의 변수의 값에 따라 분기를 하는 조건문이다.

  ```javascript
  const name = '홍길동'
  // const name = 'admin'
  
  
  switch (name) {
      case 'admin': {
        console.log('ADMIN')
      }
      case 'manager': {
          console.log('MANAGER')
      }
      default: {
          console.log(`${name}`)
      }
  }
        
  // ADMIN, MANAGER, admin
  ```
  
  - `case`에 해당하는 값이 있다면, 그 내용을 실행하면서, 그 다음도 실행하면서, defaul에서 정의한 내용도 함께 실행된다.
  - `break`와 함께 사용한다.
  
  ```javascript
  const name = '홍길동'
  // const name = 'admin'
  
  
  switch (name) {
      case 'admin': {
          console.log('ADMIN')
          break
      }
      case 'manager': {
          console.log('MANAGER')
          break
      }
      default: {
          console.log(`${name}`)
      }
  }
          
  // ADMIN, MANAGER, admin
  ```



### 03.2 반복문

#### while

- `while` 키워드 뒤에 오는 조건이 `true`인 동안 반복한다.

  ```javascript
  let i = 0
  
  while (i<6) {
      console.log(i)
      i++
  }
  ```

#### for

```javascript
for (let i = 0; i < 6; i++) {
    console.log(i)
}
```



#### for of

- 배열에서 요소를 하나씩 순회하며 반복하는 반복문이다.

- 블럭 내에서 변수로 선언되기 때문이다.

  ```javascript
  const numbers = [1,2,3,4]
  
  for (const number of numbers) {
      console.log(number)
  }
  ```

  

#### for in

- object의 key값을 순회하는 반복문이다.

- 배열의 경우 index 값을 순회한다.

  ```javascript
  const number = [1,2,3,4]
  
  for (const number in numbers) {
      console.log(number)
  }
  
  const fruits = {
      a:'apple',
      b:'banana',
  }
  
  for (const key in fruits) {
      console.log(key) // a, b
      console.log(fruits[key]) // apple, banana
  }
  ```

## 4. Functions

#### 04. 1 functions

#### 선언식

```javascript
function add (num1, num2) {
    return num1 + num2
}

add(1,3)  // 4
```



#### 표현식

- 일반적으로 표현식은 익명 함수로 작성한다.
- 익명함수는 표현식에서만 사용 가능하다.

```javascript
const sub = function (num1, num2) {
    return num1 - num2
}

sub(3, 1)
```

```javascript
const mySub = function namedSub (num1, num2) {
    return num1 - num2
}
mySub(3, 1)
// namedSub(3,1) 은 오류남.
// mySub 오류 발생시 함수가 정의된 곳(namedSub)의 위치가 이름을 알려주며 에러발생.
```



#### 기본인자

```javascript
const greeting = function (name = '홍길동') {
    return name
}
```



### 04.2 선언식 vs 표현식

```javascript
console.log(typeof add)
console.log(typeof sub)
```



#### Hoisting

```javascript
add(2, 7)

function add(num1, num2) {
    return num1 + num2
}
// 이렇게 하면 Hoisting 발생, 주의해야할 사항
```

- 표현식은 함수를 변수에 할당했고, 일종의 변수처럼 작동한다.

  ```javascript
  sub(1, 3)
  
  const sub = function(num1, num2) {
      return num1 - num2
  }
  // 얘는 Hoisting 안일어남.
  ```

- var로 function 선언시

  ```javascript
  var sub
  sub (1, 3)
  
  var sub = function (num1, num2) {
      return num1 - num2
  }
  ```



### 04.3 Arrow Function

> function과 중괄호를 생략하여서 코드를 줄이기 위해 고안된 단축 문법

	1. function 생략가능
 	2. 함수의 매개변수가 하나밖에 없다면 () 생략가능
 	3. 함수의 바디 {} 안에 들어가는 표현식이 하나면 {} return 생략가능

```javascript
const arrow = function (name) {
    return `${name}입니다.`
}

// 1. function 생략
const arrow = (name) => {
    return `${name}입니다.`
}

// 2. () 생략 가능
const arrow = name => {
    return `${name}입니다.`
}

// {}, return 생략 가능
const arrow = name => `${name}입니다.`

arrow('홍길동')
```



## Data Structure

### 05.1 Array

- 사용법

  ```javascript
  const numbers = [1,2,3,4]
  
  numbers[0]
  numbers[3]
  // numbers[-1]
  numbers.length
  ```

#### 자주 사용하는 메서드

- `push` && `pop`

  ```javascript
  numbers.push('5')  5 새로운 배열의 길이
  numbers.pop() // '5'
  ```

- `reverse` 배열을 반대로 정렬

  ```javascript
  numbers.reverse() // [4,3,2,1]
  ```

- `unshift` && `shift`

  ```javascript
  numbers.unshift('a')
  numbers // ['a', 1, 2, 3, 4]
  
  numbers.shift() // 'a' 가장 처음요소 // 빼주는 거임
  numbers
  ```

  

- `includes`

  ```javascript
  numbers.includes(1) // true
  numbers.includes(0) // false
  ```

- `indexOf`

- 배열에 특정 요소가 있는지 확인. 있으면 가장 첫번쨰로 찾은 요소의 그 `index`를 반환해요.

- 없으면 -1을 반환한다.

  ```javascript
  numbers.indexOf(1)
  numbers.indexOf(0)
  ```

- `join` 

  ```javascript
  numbers.join()
  numbers.join('')
  numbers.join('-')
  ```

  

### 05.2 Object

-  사용법

- key 같은 문자열 형태로 작성, value는 모든 형태가 작성 될 수 있다.

  ```javascript
  const person = {
      'name': '홍길동',
      'phone number': '010-1234-1234',
      pocket : {
      	phone : 'galaxy note 9',
          earphone: 'buzz live',
          'note book' : 'macbook',
      }
  }
  ```

#### 요소 접근

- dot notation

  ```javascript
  person.name // '홍길동'
  person['name']
  person['phone number']
  person.pocket // object
  person.pocket.phone
  person.pocket['phone']
  ```

#### Object 축약 문법

- 객체를 정의할 때 key 값과 할당하는 변수의 이름이 같으면 축약이 가능합니다.

  ```javascript
  const books = ['python', 'JS']
  
  const professor = {
      ggu : ['django', 'JS'],
      json: ['bk', 'nam']
  }
  
  const anything = null
  
  const hphk = {
      books,
      professor,
      anything,
  }
  
  console.log(hphk)
  ```

  ``` javascript
  const userInformation = {
      name: 'kim',
      userId: 'ggu',
  }
  ```

- ESS 이전

  ```javascript
  const name = userInformation.name
  const userId = userInformation.userId
  ```

- ES6+ 이후

  ```javascript
  const { name } = userInformation
  const {userId} = userInformation
  ```

  ```javascript
  function getUserInfo (userInformation) {
      console.log(`userName = ${userInformation.name}`)
  }
  getUserInfo(userInformation)
  
  function getUserInfo ({name}) {
      cosole.log(`userName = ${name}`)
  }
  getUserInfo(userInformation)
  ```

### 05.3 JSON(JavaScript Objecet Notation)

- key - > value 처럼 생겻는데 실제로는 문자열
- Object 처럼 쓰려면 Parsing 작업이 필요하다.

#### Object -> JSON(string)

```javascript
const jsonData = Json.stringify({
    tea : '국화차',
    coffe : '아메리카노',
})

console.log(jsonData)
console.log(typeof jsonData) // object가 아닌 string 형태.
```



#### JSON(string) -> Object(parsing)

```javascript
const parseData = JSON.parse(jsonData)

console.log(parseData) // {tea:"국화차", coffe:"아메리카노"}
console.log(typeof parseData) // object
```



### 05.4 Array Helper Method

> helper 는 일종의 라이브러리
>
> ES5.1 버전에 처음 등장. 본격적으로 사용 된 것은 ES6부터임.

#### forEach

- 주어진 `callBack`을 배열에 있는 각 요소를 오름차순으로 한번씩 실행한다.

  ```javascript
  arr.forEach(callback(element, index, array))
  ```

- EX)

  ```javascript
  const colors = ['red', 'blue', 'white']
  
  colors.forEach(function (color) {
      console.log(color)
  })
  
  colors.forEach(color => console.log.(color))
  ```

- `forEach`는 return 값이 없음.

```javascript
const result = colors.forEach(color => console.log(color))
console.log(result)
```



#### map

- 배열의 모든 요소에 대해 `callback`을 실행한다. 함수의 반환값을 요소로 하는 새로운 배열을 반환.

- 배열을 내가 원하는 다른 형식으로 바꿔야 할때쓴다.

  ```javascript
  arr.map(callback(element, index, array))
  ```

- EX)

  ```javascript
  const numbers = [1,2,3]
  
  const mapNumbers = numbers.map(function (number) {
      return number * 2
  })
  
  console.log(mapNumbers)
  ```

#### filter

- callback 함수를 실행했을 때, 어떠한 테스트 혹은 조건을 만족하고 통과하는 모든 요소를 모아서 새로운 배열을 반환한다.
- EX)

```javascript
const products = [
    { name: 'cucumber', type: 'vegetable'},
    { name: 'banana', type: 'fruit'},
    { name: 'carrot', type: 'vegetable'},
    { name: 'apple', type: 'fruit'},
]

const fruits = products.filter(function (product) {
    return product.type === 'fruit'
})

console.log(fruits)
```



#### reduce

- 배열 내의 숫자 총합, 평균 계산 배열의 하나의 값으로 줄이는 동작

  ```javascript
  arr.reduce(callback(acc, element, index, array), intialvalue)
  ```

- 첫번째 매개변수 acc는 누적값을 의미한다.

- 두번째 매개변수 initialValue는 초기 값을 의미한다.

```javascript
const tests = [90, 90, 80, 77]

const sum = tests.reduce(function (total, x) {
    return total + x
}, 0)  // 여기서 0 생략 가능

console.log(sum)
```



#### find

- `callback`을 만족하는 `첫번째 요소`를 찾아서 반환한다. 없으면 `undefined`를 반환한다.

```javascript
arr.find(callback(element, index, array))
```

- EX)

```javascript
const avengers = [
      { name: 'Tony Stark', age: 45 },
      { name: 'Steve Rogers', age: 32 },
      { name: 'Thor', age: 40 },
    ]

    const avenger = avengers.find(function (avenger) {
      return avenger.name === 'Tony Stark'
    })
```



#### some

- 배열 안의 요소 중, 단 하나라도 조건을 만족한다면 true 반환, 아니면 false 반환

```javascript
arr.some(callback(element, index, array))
```

- EX)

```javascript
const arr = [1, 2, 3, 4, 5]

const result = arr.some(elem => elem % 2 === 0)  // true
```



#### every

- 배열 안의 요소가 모두 조건을 만족해야 true 반환, 아니면 false 반환

```javascript
arr.every(callback(element, index, array))
```

- EX)

  ```javascript
  const arr = [1, 2, 3, 4, 5]
  
  const result2 = arr.every(elem => elem % 2 === 0) // false
  console.log(result2)
  ```

  