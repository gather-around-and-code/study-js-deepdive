# 7장. 연산자

연산자(operator)는 하나 이상의 표현식을 대상으로 산술, 할당, 비교, 논리, 타입, 지수 연산 등을 수행해 **하나의 값**을 만듭니다.

- **산술 연산자(arithmetic operator)**

  산술 연산자는 피연산자를 대상으로 수학적 계산을 수행해 새로운 숫자 값을 만듭니다. 
  
  산술 연산이 불가능한 경우 **`NaN`** 을 반환합니다.
  
  - **이항 산술 연산자**
    
    - **`+`** (덧셈), **`-`** (뺄셈), **`*`** (곱셈), **`/`** (나눗셈), **`%`** (나머지)
    - 2개의 피연산자를 산술 연산하여 숫자 값을 만듭니다.
    - 모든 이항 산술 연산자는 피연산자의 값을 변경하는 부수 효과가 없습니다. 즉, 피연산자의 값을 바꾸지 않고 언제나 새로운 값을 만듭니다.
    
  - **단항 산술 연산자**
      
    - **`++`** (증가), **`--`** (감소), **`+`** (어떠한 효과도 없음), **`-`** (양수를 음수로, 음수를 양수로 반전한 값을 리턴)
    - 1개의 피연산자를 산술 연산하여 숫자 값을 만듭니다.
    - 증가, 감소 연산자는 피연산자의 값을 변경하는 부수 효과가 있습니다.

      ```javascript
      var x = 1;
      
      // ++ 연산자는 피연산자의 값을 변경하는 암묵적 할당이 이뤄집니다.
      x++; // x  = x + 1;
      console.log(x); // 2
      
      // -- 연산자는 피연산자의 값을 변경하는 암묵적 할당이 이뤄집니다.
      x--; // x  = x - 1;
      console.log(x); // 1
      ```
    
    - 후위, 전위 증감 연산자

      ```javascript
      var x = 5;
      var result;
      
      // 후위 증가 연산자: 선할당 후 증가
      result = x++;
      console.log(result, x); // 5 6
      
      // 전위 증가 연산자: 선증가 후 할당
      result = ++x;
      console.log(result, x); // 7 7
      
      // 후위 감소 연산자: 선할당 후 감소
      result = x--;
      console.log(result, x); // 7 6
      
      // 전위 감소 연산자: 선감소 후 할당
      result = --x;
      console.log(result, x); // 5 5
      ```
    
    - 숫자 타입이 아닌 피연산자에 **`+`** 단항 연산자를 사용하면 피연산자를 숫자 타입으로 변환하여 반환합니다.
      이때 피연산자를 변경하지 않고 숫자 타입으로 변환한 값을 변환하여 반환합니다.

      ```javascript
      var x = '1';
      
      // 문자열을 숫자 타입으로 변환
      console.log(+x); // 1
      // 부수 효과는 없음
      console.log(x); // '1'
      
      // 불리언 값을 숫자로 타입 변환
      x = false;
      console.log(+x); // 0
      // 부수 효과는 없음
      console.log(x); // false
      
      // 문자열을 숫자로 타입 변환할 수 없으므로 NaN 반환
      x = 'Hello';
      console.log(+x); // NaN
      // 부수 효과는 없음
      console.log(x); // 'Hello'
      ```
  
  - **문자열 연결 연산자**
      
    **`+`** 연산자는 피연산자 중 하나 이상이 문자열인 경우 문자열 연결 연산자로 동작합니다.

    ```javascript
    // 문자열 연결 연산자
    '1' + 2; // '12'
    1 + '2'  // '12'

    // null은 0으로 타입 변환
    1 + null; // 1

    // undefined는 숫자로 타입 변환되지 않음
    +undefined; // NaN
    1 + undefined; // NaN
    ```

    > 개발자의 의도와 상관 없이 자바스크립트 엔진에 의해 암묵적으로 타입이 자동 변환되는 것을 **암묵적 타입 변환, 강제 타입 변환**이라고 합니다.
      
<br>
  
- **할당 연산자(assignment operator)**

  할당 연산자는 우항에 있는 피연산자의 평가 결과를 좌항에 있는 변수에 할당합니다. 좌항의 변수에 값을 할당하므로 변수 값이 변하는 부수 효과가 있습니다.
  
  - 할당문은 값으로 평가되는 표현식인 문으로서 할당된 값으로 평가됩니다.
  
    ```javascript
    var a, b;
    
    // 할당문은 표현식인 문입니다.
    console.log(a = 10); // 10
    
    // 할당문을 다른 변수에 할당할 수도 있습니다.
    console.log(a, b); // 10 10
    ```

<br>

- **비교 연산자(comparison operator)**

  비교 연산자는 좌항과 우항의 피연산자를 비교한 다음 그 결과를 불리언 값으로 반환합니다.
  
  - 동등비교 연산자
    
    좌항과 우항의 피연산자를 비교할 때 먼저 암묵적 타입 변환을 통해 타입을 일치시킨 후 같은 값인지 비교합니다.
    
    - **`==`** 동등 비교 (값만 확인) 
    - **`!=`** 부동등 비교 (값만 확인)
    
    ```javascript
    // 타입은 다르지만 암묵적 타입 변환을 통해 타입을 일치시키면 동등합니다.
    5 == '5'; // true
    
    // 동등비교는 결과를 예측하기 어렵습니다.
    0 == '';   // true
    '0' == ''; // false
    0 == '0'   // true
    false == 'false'   // false
    false == '0'       // true
    false == null;     // false
    false == undefined // false
    ```
    
  - 일치비교 연산자

    좌항과 우항의 피연산자가 타입도 같고 값도 같은 경우에 한하여 true를 반환합니다.
    
    - **`===`** 일치 비교 (타입까지 확인)
    - **`!==`** 불일치 비교 (타입까지 확인)

    ```javascript
    5 === 5;   // true
    
    // 암묵적 타입 변환을 하지 않고 값을 비교합니다.
    // 값과 타입이 모두 같은 경우만 true를 반환합니다.
    5 === '5'; // false
    
    // NaN은 자신과 일치하지 않는 유일한 값입니다.
    NaN === NaN; // false
    
    // 양의 0과 음의 0의 일치, 동등 비교 결과는 모두 true 입니다.
    0 === -0; // true
    0 == -0;  // true
    ```
  
  - 대소 관계 비교 연산자

    대소 관계 비교 연산자는 피연산자의 크기를 비교하여 불리언 값을 반환합니다.
    
    - **`>`**, **`<`**, **`>=`**, **`<=`**

- 삼항 조건 연산자

  삼항 조건 연산자는 조건식의 평가 결과에 따라 반환할 값을 결정합니다.
  
  - 조건식의 평가 결과가 불리언이 아니면 불리언 값으로 암묵적 타입 변환 됩니다.
  
  - 조건에 따라 수행해야 할 문이 여러 개라면 if - else문이 가독성이 더 좋습니다.

  ```javascript
  var result = '조건' ? 'pass' : 'fail';
  ```
  
  ```javascript
  var x = 2;

  // 2 % 2는 0이고 0은 false로 암묵적 타입 변환
  // 삼항 조건 연산자 표현식은 표현식인 문이므로, 값처럼 사용할 수 있습니다.
  var result = x % 2 ? '홀수' : '짝수';
  console.log(result); // 짝수
  ```

<br>

- **논리 연산자(logical operator)**
  
  논리 연산자는 우항과 좌항의 피연산자를 논리 연산합니다.
  
  - **`||`** (논리합 연산자), **`&&`** (논리곱 연산자), **`!`** (논리부정 연산자)
  
  - 논리 부정 연산자는 언제나 불리언 값을 반환합니다.
  
    ```javascript
    // 암묵적 타입 변환
    !0        // true
    !'Hello'; // false
    ```
  
  - 논리합 또는 논리곱 연산자 표현식의 평가 결과는 불리언 값이 아닐 수도 있습니다.

    ```javascript
    // 단축 평가
    'Cat' && 'Dog'; // Dog
    ```

<br>

- **쉼표 연산자**

  쉼표 **`,`** 연산자는 왼쪽 피연산자부터 차례대로 피연산자를 평가하고 마지막 피 연산자의 평가가 끝나면 마지막 피연산자의 평가 결과를 반환합니다.
  
  ```javascript
  var x, y, z;
  x = 1, y = 2, z = 3; // 3
  ```

<br>

- **그룹 연산자**

  소괄호 **`()`** 로 피연산자를 감싸서 표현식에서 가장 먼저 평가되도록 할 수 있습니다.
  
  ```javascript
  10 * 2 + 3;   // 23
  10 * (2 + 3); // 50
  ```

<br>

- **typeof 연산자**

  **`typeof`** 연산자는 피연산자의 데이터 타입을 문자열로 반환합니다.
  
  - string, number, boolean, undefined, symbol, object, function 중에 하나 반환합니다.
  
  - null을 반환하는 경우는 없습니다.

  ```javascript
  // typeof 연산자로 null을 연산하면 null이 아닌 object를 반환합니다.
  type of null; // object
  
  // 값이 null 타입인지 확인할 때는 typeof 연산자를 사용하지 말고 일치 연산자를 사용해야 합니다.
  var foo = null;
  typeof foo === null; // false
  foo === null;        // true
  ```

<br>

- **지수 연산자**

  ES7에서 도입된 연산자로, 좌항의 피연산자를 밑으로, 우항의 피연산자를 지수로 거듭 제곱하여 숫자 값을 반환합니다.
  
<br>

- **그 외의 연산자**

  - **`?.`** 옵셔널 체이닝 연산자
  - **`??`** null 병합 연산자
  - **`delete`** 프로퍼티 삭제
  - **`new`** 생성자 함수를 호출할 때 사용하여 인스턴스 생성
  - **`instanceof`** 좌변의 객체가 우변의 생성자 함수와 연결된 인스턴스인지 판별
  - **`in`** 프로퍼티 존재 확인

<br>

- **연산자의 부수 효과**
  
  - 대부분의 연산자는 다른 코드에 영향을 주지 않습니다.
  - **`=`**, **`++`**, **`--`**, **`delete`** 연산자는 부수 효과가 있는 연산자 입니다.

<br>

- **연산자의 우선순위**

  연산자 우선순위란 여러 개의 연산자로 이뤄진 문이 실행될 때 연산자가 실행되는 순서를 말합니다. 우선순위가 높을수록 먼저 실행됩니다.
  
<br>

- **연산자의 결합순서**

  연산자 결합 순서란 연산자의 어느 쪽(좌항 또는 우항)부터 평가를 수행할 것인지를 나타내는 순서를 말합니다.
