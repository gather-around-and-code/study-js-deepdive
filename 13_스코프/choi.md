# 13장. 스코프

## 스코프란?
스코프(유효범위 scope)는 자바스크립트를 포함한 모든 프로그래밍 언어의 기본적이며 중요한 개념이다.
스코프는 변수 그리고 함수와 깊은 관련이 있다. 
- var, let, const키워드로 선언한 변수의 스코프가 다르게 동작한다.
- 함수의 매개변수는 함수 몸체 내부에서만 참조할 수 있고 함수 몸체 외부에서는 참조할 수 없다. 매개변수의 스코프가 함수 몸체 내부로 한정되기 때문이다.

``` javascript

// 코드의 가장 바깥 영역에서 선언한 변수
var var1 = 1; 

if (true){
    // 코드 블록 내에서 선언한 변수
    var var2 = 2;
    if(true){
        // 중첩된 코드 블록 내에서 선언한 변수
        var var3 = 3;
    }
}

function foo(){
    var var4 = 4; // 함수 내에서 선언한 변수

    function bar(){
        var var5 = 5; // 중첩된 함수 내에서 선언한 변수
    }
}

console.log(var1); // 1
console.log(var2); // 2
console.log(var3); // 3
console.log(var4); // ReferenceError : var4 is not defined
console.log(var5); // ReferenceError : var5 is not defined

```
모든 식별자(변수이름, 함수이름, 클래스 이름 등)는 자신이 선언된 위치에 의해 다른 코드가 식별자 자신을 참조할 수 있는 유효 범위가 결정된다.
이를 스코프라 한다. 즉, 스코프는 식별자가 유효한 범위를 말한다.

식별자 결정 : 자바스크립트 엔진은 이름이 같은 두개의 변수 중에서 어떤 변수를 참조해야 할 것인지를 결정한다.
따라서 스코프란 자바스크립트 엔진이 식별자를 검색할 때 사용하는 규칙이라고도 할 수 있다.

```javascript

var x = 'global';

function foo(){
    var x = 'local';
    console.log(x);
}
foo(); // local

console.log(x); // global 

```
위 예제에서 선언된 변수 x는 식별자 이름이 동일하지만 자신이 유효한 번위, 즉 스코프가 다른 별개의 변수다. 
만약 스코프라는 개념이 없다면 같은 이름을 갖는 변수는 충돌을 일으키므로 프로그램 전체에서 하나밖에 사용할 수 없다. 스코프 내에서 식별자는 유일해야 하지만 다른 스코프에는 같은 이름의 식별자를 사용할 수 있다. 즉 스코프는 네임스페이스다.

#### 코드의 문맥과 환경
'코드가 어디서 실행되며 주변에 어떤 코드가 있는지'를 렉시컬 환경이라고 부른다. 코드의 문맥은 렉시컬 환경으로 이뤄진다. 이를 구현한 것이 '실행 컨텍스트'이며, 모든 코드는 실행 컨텍스트에서 평가되고 실행된다.

#### var 키워드로 선언한 변수의 중복 선언
```javascript
function foo(){
    var x = 1;
    // var 키워드로 선언된 변수는 같은 스코프 내에서 중복 선언을 허용한다.
    var x = 2;
    console.log(x); // 2
}

function bar(){
    let x = 1;
    // let이나 const 키워드로 선언된 변수는 같은 스코프 내에서 중복 선언을 허용하지 않는다.
    let x = 2; // SyntaxError
}
```
<br>

## 스코프의 종류
코드는 전역과 지역으로 구분할 수 있다.
변수는 자신이 선언된 위치에 의해 자신이 유효한 범위인 스코프가 결정된다.

### 전역과 전역 스코프
- 전역이란 코드의 가장 바깥 영역을 말한다. 
- 전역은 전역 스코프를 만든다. 
- 전역에 변수를 선언하면 전역 스코프를 갖는 전역 변수가 된다. 
- 전역변수는 어디서든지 참조할 수 있다.

### 지역과 지역 스코프
- 지역이란 함수 몸체 내부를 말한다. 
- 지역은 지역 스코프를 만든다.
- 지역에 변수를 선언하면 지역 스코프를 갖는 지역 변수가 된다.
- 지역변수는 자신이 선언된 지역과 하위지역(중첩함수)에서만 참조할 수 있다. (자신의 지역스코프와 하위 지역 스코프에서 유효하다)


## 스코프 체인
스코프가 계층적으로 연결된 것을 스코프 체인이라 한다.
변수를 참조할 때 자바스크립트 엔진은 스코프 체인을 통해 변수를 참조하는 코드의 스코프에서 시작하여 상위 스코프 방향으로 이동하며 선언된 변수를 검색한다. 이를 통해 상위 스코프에서 선언한 변수를 하위 스코프에서도 참조할 수 있다.

#### 렉시컬 환경
스코프 체인은 실행 컨텍스트의 렉시컬 환경을 단방향으로 연결한 것이다. 전역 렉시컬 환경은 코드가 로드되면 곧바로 생성되고 함수의 렉시컬 환경은 함수가 호출되면 곧바로 생성된다.

### 스코프 체인에 의한 변수 검색
자바스크립트 엔진은 스코프 체인은 따라 변수를 참조하는 코드의 스코프에서 시작해서 상위 스코프 방향으로 이동하며 선언된 변수를 검색한다.
절대 하위 스코프로 내려가면서 식별자를 검색하는 일은 없다. 스코프 체인으로 연결된 스코프의 계층적 구조는 부자 관계로 이뤄진 상속과 유사하다.

### 스코프 체인에 의한 함수 검색
```javascript
function foo(){
    console.log('global function foo');
}

function bar(){
    function foo(){
        console.log('local function foo');
    }
    foo();
}

bar();
```
함수도 식별자에 해당되기 때문에 스코프를 갖는다. 사실 함수는 식별자에 함수 객체가 할당된 것 외에는 일반 변수와 다를 바 없다. 
따라서 스코프를 "변수에 검색할 때 사용하는 규칙"이라고 표현하기 보다는 "식별자를 검색하는 규칙"이라고 표현하는 것이 더 적합하다.


## 함수 레벨 스코프

지역은 함수 몸체 내부를 말하고 지역은 지역 스코프를 만든다고 했다. 이는 코드 블록이 아닌 함수에 의해서만 지역 스코프가 생성된다는 의미다.
var 키워드로 선언된 변수는 오로지 함수의 코드 블록(함수 몸체)만을 지역 스코프로 인정한다. 이를 함수 레벨 스코프라 한다.

```javascript

var x = 1;
if(true){
    // 이미 선언된 전역변수 x가 있으므로 x변수는 중복선언된다. 의도치 않게 변수 값이 변경되는 부작용을 발생시킨다.
    var x = 10;
}
console.log(x); // 10

var i = 10;
for (var i = 0; i < 5; i++;){
    console.log(i) // 0 1 2 3 4 
}

// 의도치 않게 변수의 값이 변경되었다.
console.log(i); // 5

```
var 키워드로 선언된 변수는 오로지 함수의 코드 블록 만이 지역 슼프로 인정하지만, ES6에서 도입된 let, const 키워드는 블록 레벨 스코프를 지원한다.


## 렉시컬 스코프

```javascript

var x = 1;

function foo() {
    var x = 10;
    bar();
}

function bar() {
    console.log(x);
}

foo(); //
bar(); //

```

1. 동적 스코프 : 함수를 어디서 호출했는지에 따라 함수의 상위 스코프를 결정한다.
함수를 정의하는 시점에는 함수가 어디서 호출될지 알 수 없다. 따라서 함수가 호출되는 시점에는 상위 스코프를 결정해야 하기 때문에 동적 스코프라 부른다.

2. 렉시컬 스코프 또는 정적 스코프 : 동적 스코프 방식처럼 상위 스코프라 동적으로 변하지 않고 함수 정의가 평가되는 시점에 상위 스코프가 정적으로 결정되기 때문에 정적 스코프라 부른다.


자바스크립트는 렉시컬 스코프를 따르므로 함수를 어디서 호출했는지가 아니라 함수를 어디서 정의했는지에 따라 상위 스코프를 결정한다. 함수가 호출된 위치는 상위 스코프 결정에 어떠한 영향을 주지 않는다. 

이처럼 함수의 상위 스코프는 함수 정의가 실행될 때 정적으로 결정된다. 함수정의가 실행되어 생성된 함수 객체는 이렇게 결정된 상위 스코프를 기억한다. 함수가 호출될 떄마다 함수의 상위 스코프를 참조할 필요가 있기 때문이다.