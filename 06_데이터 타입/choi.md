# 6장. 데이터 타입

- **데이터타입(줄여서 '타입') = 값의 종류**

  자바스크립트는의 **모든 값은 데이터 타입을 갖는다.** 총 7개의 데이터타입을 제공하며, 원시타입과 객체타입으로 분류할 수 있다.

  - 원시타입
    - 숫자타입(number)
    - 문자열타입(string)
    - 불리언타입(boolean)
    - undefined 타입
    - null 타입
    - 심벌타입(symbol)
  - 객체타입
    - 객체
    - 함수
    - 배열 등..  
  
  <br>

  
  - **숫자타입**

  자바스트립트는 독특하게 하나의 숫자 타입만 존재한다. 
  숫자 타입은 배정밀도 64비트 부동소수점 형식을 따른다. 즉, **모든 수를 실수로 처리**하며, 정수만 표현하기 위한 데이터 타입이 별도로 존재하지 않는다.
  
  ```javascript
  // 모두 숫자타입이다. integer은 정수, double은 실수, negative는 음의 정수
  var integer = 10;
  var double = 5.28;
  var negative = -30;
  ```
  
  > 정수, 실수, 2진수, 8진수, 16진수 리터럴은 모두 메모리에 배정밀도 64비트 부동소수점 형식의 2진수로 저장된다. 자바스크립트는 2진수, 8진수, 16진수를 표현하기 위한 데이터 타입을 제공하지 않기 때문에 이들값을 참조하면 모두 10진수로 해석된다.

  자바스크립트의 숫자 타입은 정수만을 위한 타입이 없고 모든 수를 실수로 처리한다고 했다. 이는 정수로 표시된다 해도 사실은 실수라는 것을 의미한다. 따라서 정수로 표시되는 수끼리 나누더라도 실수가 나올수 있다.

  ```javascript
  // 숫자 타입은 모두 실수로 처리된다.
  console.log(1 === 1.00);
  console.log(4 / 2); // 2
  console.log(3 - 0.5) // 2.5
  ```
  
  **숫자타입은 추가적으로 3가지 특별한 값도 표현할 수 있다.**
  - Infinity : 양의 무한대
  - -Infinity : 음의 무한대
  - NaN : 산술연산 불가 (not-a-number)

  > 자바스크립트는 대소문자를 구별하므로 NaN을 NAN, Nan, nan과 같이 표현하면 에러가 발생하므로 주의해야한다. 

<br>

- **문자열타입**
  
  텍스트 데이터를 나타내는데 사용한다. 문자열은 0개 이상의 16비트 유니코드 문자(UTF-16)의 집합으로 **전세계 대부분의 문자를 표현할 수 있다.**
  문자열은 **`작은따옴표('')`**, **`큰 따옴표("")`**, **`백틱(``)`**으로 텍스트를 감싼다. 
  
    ```javascript

    let string;

    string = '문자열';
    string = "문자열";
    string = `문자열`;
    
    // 따옴표로 감싸지 않은 문자열은 식별자 같은 토큰으로 인식한다. 
    // 또한 따옴표로 문자열을 감싸지 않는다면 스페이스와 같은 공백 문자도 포함시킬 수 없다.
    // 문자열은 원시타입으로 변경 불가능한 값이다. 

    ```

<br>

- **템플릿 리터럴**
  
  ES6부터 새로운 문자열 표기법이 도입.
  멀티라인 문자열, 표현식 삽입, 태그드 템플릿 등 편안한 문자열 처리 기능 제공. 
  일반 문자열과 비슷해 보이지만 일반적이 따옴표대신 백틱(``)을 사용해 표현.

  **멀티라인 문자열**

  일반 문자열 내에서 줄바꿈 등의 공백을 표현하려면 백슬래시(\)로 시작하는 이스케이프 시퀀스를 사용해야한다.

  ```javascript
     
     let templet = `<ul>
        <li><a href="#"></a></li>
    </ul>`

    console.log(templet);    
  ```

  **표현식 삽입**

  일반 문자열은 연산자 +를 사용해 연결할 수 있다. 표현식은 삽입하려면 ${}으로 표현식을 감싼다.

  ```javascript

  let first = "Da yeon";
  let last = "Choi";

    // 문자열 연결 
    console.log('my name is ' + first + ' ' + last + '.');

    //표현식 삽입
    console.log(`my name is ${first} ${last}.`);

    // 표현식의 평가 결과가 문자열이 아니더라도 문자열로 타입이 강제로 변환되어 삽입된다.
  ```  
<br>

- **불리언 타입**
  
  논리적 참, 거짓을 나타내는 true와 false뿐이다.
  프로그램 흐름을 제어하는 **조건문에서 자주 사용**한다.
  
  
<br>

- **undefined 타입**
  
  undefined 타입의 값은 undefined가 유일하다. 
  var 키워드로 선언한 변수는 암묵적으로 undefined로 초기화된다.
  자바스크립트 엔진이 변수를 초기화하는 데 사용하는 undefined를 개발자가 의도적으로 변수에 할당한다면 undefined의 본래 취지와 어긋날뿐더러 혼란을 줄 수 있으므로 권장하지 않는다. 변수에 값이 없다는 것을 명시하고 싶을 때는 null을 할당한다.
  
<br>

- **null 타입**
  
  null타입의 값은 null이 유일하다. 변수에 값이 없다는 것을 의도적으로 명시할 때 사용한다. 이전에 참조하던 값을 더 이상 참조하지 않겠다는 의미다. 
  
  ```javascript
  var name = 'choi'; 
  name = null;     // 이전 참조를 제거. name변수는 더이상 choi를 참조하지 않는다. 
  ```  
<br>

- **심벌 타입**

ES6에서 추가된 7번째 타입. 심벌값은 다른값과 중복되지 않는 유일무이한 값이다. 주로 이름이 충돌할 위험이 없는 객체의 유일한 프로퍼티 키를 만들기 위해 사용한다. 심벌은 Symbol 함수를 호출해 생성한다. 이때 생성된 심벌값은 외부에 노출되지 않는다. 
심볼타입은 new 연산자를 이용하여 래퍼 객체를 생성하려고 하면 TypeError가 발생한다. new 연산자를 이용할 수 없다는 것은 곧 Symbol 함수를 생성자로 사용할 수 없음을 의미한다.

```javascript
  var key = Symbol('key');
  var obj = {};

  obj[key] = 'value'; //이름이 충돌한 위험이 없는 유일무이한 값인 심벌을 프로퍼티 키로 사용한다. 
  console.log(obj[key]); // value


  // Symbol 함수를 호출하면 매번 새로운(고유한) 심볼이 생성된다.
  const sym1 = Symbol();
  const sym2 = Symbol();
  const sym3 = Symbol('foo');
  const sym4 = Symbol('foo');

  console.log(sym1 === sym1);  // true
  console.log(sym1 === sym2);  // false
  console.log(sym3 === sym4);  // false

  ```  

<br>

- **객체 타입**

객체는 바로 오브젝트 { } 안에 Key와 Value 형태의 데이터가 여러 개의 형태로 복합적으로 담겨 있다고 보면 된다.

```javascript

let House = {
    address: 'Seoul',
    Apartment: 'Han',
    zipCode: 10000,
};
 
console.log(House); // { address: 'Seoul', Apartment: 'Han', zipCode: 10000 }
console.log(House.Apartment); // Han
console.log(House.address); // Seoul
console.log(House.zipCode); // 10000

```
<br>

-**원시 타입과 객체 타입 차이**

- 원시 타입은 값 자체가 메모리 셀에 들어가 있다. 원시 타입은 값이 복사되어 전달된다. (Copy by Value)
- 객체 타입은 참조값 즉 메모리 주소가 변수에 들어가 있다. 객체 타입은 참조값이 복사되어 전달된다. (Copy by Reference)

<br>

-**데이터 타입의 필요성**

**데이터 타입에 의한 메모리 공간의 확보와 참조**

값은 메모리에 저장하고 참종할 수 있어야 한다. 메모리에 값을 저장하려면 먼저 확보해야 할 메모리 공간의 크기를 결정해야한다. 몇 바이트의 메모리 공간을 사용해야 낭비와 손실 없이 값을 저장할 수 있는지 알아야한다. 
자바스크립트는 값의 종류에 따라 정해진 크기의 메모리 공간을 확보한다. 즉 데이터 타입에 따라 확보해야 할 메모리 공간의 크기가 결정된다.

<br>

**데이터 타입에 의한 값의 해석**

메모리에서 읽어 들인 2진수를 어떻게 해석하는가?
데이터 타입에 따라 2진수를 해석하는 것이 달라진다.

- 값을 저장할 때 확보해야 하는 메모리 공간의 크기를 결정하기 위해
- 값을 참조할 때 한 번에 읽어 들여야 할 메모리 공간을 크기를 결정하기 위해
- 메모리에서 읽어 들인 2진수를 어떻게 해설할지 결정하기 위해

<br>

-**동적 타이핑**

**동적타입 언어와 정적타입 언어**

변수는 데이터 타입을 가질까? 기본적으로 변수는 타입을 갖지 않는다. 하지만 값은 타입을 갖는다. 
따라서 현재 변수에 할당되어 있는 값에 의해 변수의 타입이 동적으로 결정된다고 표현하는 것이 적절하다.

- 정적타입 언어
    - 정적타입 언어는 변수를 선언할 때 변수에 할당할 수 있는 값의 데이터타입을 선언해야한다(명시적타입선언).
    - 변수 선언 시점에 변수의 타입이 결정되고 변수의 타입을 변경할 수 없다. 
    - 컴파일 시점에서 타입 체크수행. 더욱 안정적인 코드이 구현을 통해 런타임에 발생하는 에러를 줄인다.
    - C, C++, 자바, 코들린, 고, 하스켈, 러스트, 스칼라 등이 있다

- 동적타입 언어
    - 어떠한 데이터 타입의 값이라도 자유롭게 할당할 수 있다.
    - typeof 연산자는 변수의 데이터 타입을 반환하는 것이 아니라 변수에 할당된 값의 데이터타입을 반환하는 것이다.
    - 값을 할당하는 기점에 변수의 타입이 동적으로 결정되고 변수의 타입을 언제든지 자유롭게 변경할 수 있다.(동적 타이핑)
    - 할당에 의해 타입이 결정(타입 추론).
    - 자바스크립트, 파이썬, PHP, 루비, 리스프, 펄 등이 있다.

    <br>

**동적 타입 언어와 변수**

변수 값은 언제든지 변경될 수 있기 때문에 복잡한 프로그램에서는 변화하는 변수 값을 추적하기 어려울 수 있다.
더욱이 자바스크립트 개발자의 의도와는 상관없이 자바스크립티 엔진에 의해 암묵적으로 타입이 자동으로 변환되기도 한다.
동적타입 언어는 유연성은 높지만 신뢰성은 떨어진다.

- 변수를 사용할 대 주의사항
    - 변수는 꼭 필요한 경우에 한해 제한적으로 사용한다. 변수의 무분별한 남발은 금물.
    - 변수의 유효범위(스코프)는 최대한 좁게 만들어 변수의 부작용을 억제해야한다.
    - 전역변수를 최대한 사용하지 않도록 한다. 
    - 변수보다는 상수를 사용해 값의 변경을 억제한다. 
    - 변수의 이름은 목적이나 의미를 파악할 수 있도록 네이밍한다.

> 사람이 이해할 수 있는 코드, 즉 가독성이 좋은 코드가 좋은 코드다.

<br>

**스코프**

Scope를 우리말로 번역하면 ‘범위’라는 뜻을 가지고 있다. 즉, 스코프(Scope)란 ‘변수에 접근할 수 있는 범위’라고 할 수 있다.
자바스크립트에선 스코프는 2가지 타입이 있다. 바로 global(전역)스코프와 local(지역)스코프이다.


```javascript

var a = 1; // 전역 스코프
function print() { // 지역(함수) 스코프
 var a = 111;
 console.log(a);
}
print(); // 111
console.log(a); // 1

```

<br>




-**참고**

- 심볼타입 https://it-eldorado.tistory.com/149
- 원시타입과 객체타입의 차이 https://seons-dev.tistory.com/entry/JAVASCRIPT-%EC%9B%90%EC%8B%9C-%ED%83%80%EC%9E%85%EA%B3%BC-%EA%B0%9D%EC%B2%B4-%ED%83%80%EC%9E%85-%EC%B0%A8%EC%9D%B4-%EC%A0%95%EB%A6%AC
- 스코프 https://medium.com/@su_bak/javascript-%EC%8A%A4%EC%BD%94%ED%94%84-scope-%EB%9E%80-bc761cba1023