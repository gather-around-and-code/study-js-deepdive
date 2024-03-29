# 7장. 연산자(Operator)

값을 조작하거나 조건을 평가하기 위해 사용되는 기호나 키워드입니다. 연산자는 피연산자(operand)라고 불리는 값을 가지고 동작하며, 피연산자의 개수에 따라 단항 연산자(unary operator), 이항 연산자(binary operator), 삼항 연산자(ternary operator)로 분류될 수 있습니다.

**[목차]**
- **7장. 연산자(Operator)**
  - [7-1. 산술 연산자(Arithmetic Operators)](#7-1-산술-연산자arithmetic-operators)
  - [7-2. 할당 연산자(Assignment Operators)](#7-2-할당-연산자assignment-operators)
  - [7-3. 비교 연산자(Comparison Operators)](#7-3-비교-연산자comparison-operators)
  - [7-4. 논리 연산자(Logical Operators)](#7-4-논리-연산자logical-operators)
  - [7-5. 비트 연산자(Bitwise Operators)](#7-5-비트-연산자bitwise-operators)
  - [7-6. 조건(삼항) 연산자(Conditional (Ternary) Operator)](#7-6-조건삼항-연산자conditional-ternary-operator)
  - [7-7. 타입 연산자(Type Operators)](#7-7-타입-연산자type-operators)
  - [요약](#요약)
  - [키워드](#키워드)
  - [Reference](#reference)


- **단항 연산자 (Unary Operators)**:
  - `+` (양수)
  - `-` (음수)
  - `++` (증가)
  - `--` (감소)
  - `!` (논리 부정)
- **이항 연산자 (Binary Operators)**:
    - `+` (덧셈)
    - `-` (뺄셈)
    - `*` (곱셈)
    - `/` (나눗셈)
    - `%` (나머지)
    - `===` (일치 비교)
    - `!==` (불일치 비교)
    - `>` (크다)
    - `<` (작다)
    - `>=` (크거나 같다)
    - `<=` (작거나 같다)
    - `&&` (논리곱)
    - `||` (논리합)
- **삼항 연산자 (Ternary Operator)**:
    ```jsx
    condition ? expression1 : expression2
    ```

## 7-1. 산술 연산자(Arithmetic Operators)
```jsx
let a = 5;
let b = 3;
let sum = a + b;  // sum 변수에 a와 b를 더한 값을 할당

console.log(sum);  // 출력: 8
```
산술 연산자는 주어진 피연산자들 사이에서 산술 연산을 수행하고 그 결과를 반환합니다.
```jsx
let sum = 10 + 5;  // 15
let difference = 10 - 5;  // 5
let product = 10 * 5;  // 50
let quotient = 10 / 5;  // 2
let remainder = 10 % 3;  // 1
```
- 덧셈(Addition) 연산자(`+`): 두 개의 값을 더합니다.
- 뺄셈(Subtraction) 연산자(`-`): 두 개의 값을 뺍니다.
- 곱셈(Multiplication) 연산자(`*`): 두 개의 값을 곱합니다.
- 나눗셈(Division) 연산자(`/`): 첫 번째 값을 두 번째 값으로 나눕니다.
- 나머지(Modulus) 연산자(`%`): 첫 번째 값을 두 번째 값으로 나눈 후의 나머지를 반환합니다.

```jsx
let x = 5;
console.log(x++);  // 출력: 5 (후위 증가 연산자는 현재 값을 반환한 후 1을 증가시킴)
console.log(x);    // 출력: 6 (증가된 값이 출력됨)
```
- 증가(Increment) 연산자(`++`): 변수의 값을 1씩 증가시킵니다.
- 감소(Decrement) 연산자(`--`): 변수의 값을 1씩 감소시킵니다.
> 증가 연산자와 감소 연산자는 수행하는 동안 다른 상태나 변수에 영향을 미치는 것을 의미하는 부수효과(side effect)를 가집니다.

## 7-2. 할당 연산자(Assignment Operators)
할당 연산자(Assignment Operators)는 변수에 값을 할당하는 데 사용됩니다. 할당 연산자는 변수에 값을 할당하는 동시에 다른 연산을 수행할 수 있습니다. 이러한 연산은 부수효과(side effect)를 일으킬 수 있습니다

```jsx
let a = 10;

a += 5;  // a = a + 5;와 동일한 의미, 
console.log(a); // a는 이제 15

a -= 3;  // a = a - 3;와 동일한 의미, 
console.log(a); // a는 이제 12

a *= 2;  // a = a * 2;와 동일한 의미, 
console.log(a); // a는 이제 24

a /= 4;  // a = a / 4;와 동일한 의미,
console.log(a); // a는 이제 6

a %= 5;  // a = a % 5;와 동일한 의미,
console.log(a); // a는 이제 1

```
- 할당 연산자 (`=`): 오른쪽에 있는 값을 왼쪽에 있는 변수에 할당합니다.
- 덧셈 할당 연산자 (`+=`): 오른쪽에 있는 값을 왼쪽에 있는 변수에 더하고 그 결과를 변수에 할당합니다.
- 뺄셈 할당 연산자 (`-=`): 오른쪽에 있는 값을 왼쪽에 있는 변수에서 빼고 그 결과를 변수에 할당합니다.
- 곱셈 할당 연산자 (`*=`): 오른쪽에 있는 값을 왼쪽에 있는 변수와 곱하고 그 결과를 변수에 할당합니다.
- 나눗셈 할당 연산자 (`/=`): 왼쪽에 있는 변수를 오른쪽에 있는 값으로 나눈 후 결과를 변수에 할당합니다.
- 나머지 할당 연산자 (`%=`): 왼쪽에 있는 변수를 오른쪽에 있는 값으로 나눈 후 나머지를 계산하여 변수에 할당합니다.


## 7-3. 비교 연산자(Comparison Operators)
비교 연산자(Comparison Operators)는 두 개의 값을 비교하고, 비교 결과에 따라 불리언(Boolean) 값을 반환하는 연산자입니다.
```jsx
let a = 5;
let b = 3;
let c = "5";

console.log(a > b);    // 출력: true (5는 3보다 큼)
console.log(a < b);    // 출력: false (5는 3보다 작지 않음)
console.log(a >= b);   // 출력: true (5는 3보다 크거나 같음)
console.log(a <= b);   // 출력: false (5는 3보다 작거나 같지 않음)

console.log(a == c);   // 출력: true (느슨한 동등 비교, 값은 동일)
console.log(a === c);  // 출력: false (엄격한 동등 비교, 타입이 다름)
console.log(a != c);   // 출력: false (느슨한 불일치 비교, 값은 동일)
console.log(a !== c);  // 출력: true (엄격한 불일치 비교, 타입이 다름)

let x = 10;
let y = 20;
let z = 30;

console.log((x < y) && (y < z));  // 출력: true (두 조건이 모두 참)
console.log((x > y) || (y < z));  // 출력: true (하나 이상의 조건이 참)
```

- **동등 비교 연산자(Equal Operators)**:
  - `==`: 두 값이 동등한지 확인합니다. 타입 변환을 수행하며, 값이 같으면 true를 반환합니다.
  - `!=`: 두 값이 동등하지 않은지 확인합니다. 타입 변환을 수행하며, 값이 다르면 true를 반환합니다.
- **일치 비교 연산자(Strict Equal Operators)**:
  - `===`: 두 값이 정확하게 일치하는지 확인합니다. 타입과 값이 모두 같아야 true를 반환합니다.
  - `!==`: 두 값이 일치하지 않는지 확인합니다. 타입 또는 값이 다르면 true를 반환합니다.
- **대소 관계 비교 연산자(Relational Operators)**:
  - `>`: 왼쪽 값이 오른쪽 값보다 큰지 확인합니다.
  - `<`: 왼쪽 값이 오른쪽 값보다 작은지 확인합니다.
  - `>=`: 왼쪽 값이 오른쪽 값보다 크거나 같은지 확인합니다.
  - `<=`: 왼쪽 값이 오른쪽 값보다 작거나 같은지 확인합니다.
- **논리 연산자(Logical Operators)**와 함께 사용되는 비교 연산자:
    - `&&` (논리곱): 두 비교식이 모두 true인지 확인합니다. 모두 true이면 true를 반환하고, 그렇지 않으면 false를 반환합니다.
    - `||` (논리합): 두 비교식 중 하나 이상이 true인지 확인합니다. 하나 이상 true이면 true를 반환하고, 둘 다 false이면 false를 반환합니다.

## 7-4. 논리 연산자(Logical Operators)
논리 연산자(Logical Operators)는 논리적인 조건을 결합하거나 조작하는 데 사용되는 연산자입니다. 

- **논리곱 연산자 (AND Operator) (`&&`)**: 두 개의 조건이 모두 true인지 확인합니다. 두 개의 조건이 모두 true일 때, 전체 표현식은 true를 반환하고, 그렇지 않으면 false를 반환합니다.
    ```jsx
    let a = 10;
    let b = 5;
    let c = 3;

    console.log(a > b && b > c);  // 출력: true (두 개의 조건이 모두 참)
    console.log(a > b && b < c);  // 출력: false (두 개의 조건 중 하나가 거짓)
    ```
- **논리합 연산자 (OR Operator) (`||`)**: 두 개의 조건 중 하나 이상이 true인지 확인합니다. 하나 이상의 조건이 true일 때, 전체 표현식은 true를 반환하고, 두 개의 조건이 모두 false이면 false를 반환합니다.
  ```jsx
    let a = 10;
    let b = 5;
    let c = 3;

    console.log(a > b || b > c);  // 출력: true (두 개의 조건 중 하나가 참)
    console.log(a < b || b < c);  // 출력: false (두 개의 조건이 모두 거짓)
  ```
- **논리 부정 연산자 (NOT Operator) (`!`)**: 주어진 조건의 부정을 반환합니다. 주어진 조건이 true면 false를, 주어진 조건이 false면 true를 반환합니다.
    ```jsx
    let a = 10;
    let b = 5;

    console.log(!(a > b));  // 출력: false (주어진 조건의 부정)
    console.log(!(a < b));  // 출력: true (주어진 조건의 부정)
    ```

## 7-5. 비트 연산자(Bitwise Operators)
## 7-6. 조건(삼항) 연산자(Conditional (Ternary) Operator)
JavaScript에서 사용되는 단축 표현식으로, 세 개의 피연산자를 기반으로 조건을 판단하여 값을 반환합니다.

```jsx
조건식 ? 참일 때 반환할 값 : 거짓일 때 반환할 값
```
조건식이 참이면 첫 번째 피연산자가 반환되고, 조건식이 거짓이면 두 번째 피연산자가 반환됩니다.
```jsx
let number = 10;
let result = number > 0 ? "양수" : "음수";

console.log(result);  // 출력: "양수"
```
조건(삼항) 연산자는 if-else 문을 간결하게 표현할 수 있고, 조건에 따라 서로 다른 값을 반환하거나 변수에 할당하는 등 다양한 상황에서 사용됩니다.

## 7-7. 타입 연산자(Type Operators)

## 요약

1. 산술 연산자(Arithmetic Operators): 숫자 값을 가지고 산술 계산을 수행합니다.
   - `+` (덧셈)
   - `-` (뺄셈)
   - `*` (곱셈)
   - `/` (나눗셈)
   - `%` (나머지)
   - `++` (증가 연산자)
   - `--` (감소 연산자)
  
2.  할당 연산자(Assignment Operators): 변수에 값을 할당합니다.
    - `=` (할당)
    - `+=` (덧셈 후 할당)
    - `-=` (뺄셈 후 할당)
    - `*=` (곱셈 후 할당)
    - `/=` (나눗셈 후 할당)
    - `%=` (나머지 후 할당)

3. 비교 연산자(Comparison Operators): 두 값의 비교 결과를 평가하여 불리언 값을 반환합니다.
    - `==` (동등 비교)
    - `!=` (부등 비교)
    - `===` (일치 비교)
    - `!==` (불일치 비교)
    - `>` (크다)
    - `<` (작다)
    - `>=` (크거나 같다)
    - `<=` (작거나 같다)
  
4. 논리 연산자(Logical Operators): 논리적인 조건을 평가하고 불리언 값을 반환합니다.
   - `&&` (논리곱)
   - `||` (논리합)
   - `! `(논리 부정)
  
5. 비트 연산자(Bitwise Operators): 이진 비트 수준에서 값을 조작합니다.
   - `&` (비트 AND)
   - `|` (비트 OR) 
   - `^` (비트 XOR) 
   - `~` (비트 NOT) 
   - `<<` (왼쪽 시프트)
   - `>>` (오른쪽 시프트)
   - `>>>` (부호 없는 오른쪽 시프트)

6. 조건(삼항) 연산자(Conditional (Ternary) Operator): 조건에 따라 다른 값을 반환합니다.
    ```jsx
    condition ? expression1 : expression2
    ```
7. **타입 연산자(Type Operators)**: 값의 타입을 평가하고 확인합니다.
   - `typeof` (값의 타입을 문자열로 반환)
   - `instanceof` (객체의 타입을 확인)

## 키워드
## Reference