# 18장. 함수와 일급 객체


## 18.1 일급객체

다음과 같은 조건을 만족하는 객체를 일급 객체라 한다.

1. 무명의 리터럴로 생성할 수 있다. 즉, 런타임에 생성이 가능하다.
2. 변수나 자료구조(객체, 배열 등)에 저장할 수 있다.
3. 함수의 매개변수에 전달할 수 있다.
4. 함수의 반환값으로 사용할 수 있다.


``` javascript

// 1. 무명의 리터럴로 생성할 수 있다.
// 2. 변수에 저장할 수 있다.
const increase = function (num){
    return ++num;
};

const decrease = function (num){
    return --num;
};

// 2. 객체에 저장할 수 있다.
const auxs = {increase, decrease};

// 3. 매개변수에 저장할 수 있다.
// 4. 함수의 반환값으로 사용할 수 있다.
function makeCounter(aux){
    let num = 0;

    return function(){
        num = aux(num);
        return num;
    }
}

// 3. 매개변수에게 함수를 전달할 수 있다.
const increaser = makeCounter(auxs.increase);
console.log(increaser());
console.log(increaser());

const decreaser = makeCounter(auxs.decrease);
console.log(decrease());
console.log(decrease());


```

함수가 일급객체라는 것은 함수를 객체와 동일하게 사용할 수 있다는 의미다. 객체는 값이므로 함수는 값과 동일하게 취급할 수 있다.
따라서 함수는 값을 사용할 수 있는 곳(변수 할당문, 객체의 프로퍼티 값, 배열요소, 함수 호출의 인수, 함수 반환문)이라면 어디든지 리터럴로 정의할 수 있으며 런타임에 함수 객체로 평가된다.
<br>
일급 객체로서 함수가 가지는 가장 큰 특징은 일반 객체와 같이 함수의 매개변수에 전달할 수 있으며, 함수의 반환값으로 사용할 수 있는 것이다. 이는 함수형 프로그래밍을 가능케 하는 자바스크립트의 장점 중 하나다.
<br>
함수는 객체지만 일반 객체와는 차이가 있다. 일반 객체는 호출할 수 없지만, 함수 객체는 호출할 수 있다. 그리고 함수 객체는 일반 객체에는 없는 함수 고유의 프로퍼티를 소유한다.


## 18.2 함수 객체의 프로퍼티

함수객체의 내부를 들여다보자.

```javascript

function square(number){
    return number * number;
}

console.dir(square);

// ƒ square(number)
// arguments:null
// caller:null
// length:1
// name:"square"
// prototype:
// constructor:ƒ square(number)
// [[Prototype]]:Object
// [[FunctionLocation]]:VM66:1
// [[Prototype]]:ƒ ()
// [[Scopes]]:Scopes[1]



// Object.getOwnPropertyDescriptors 메서드로 확인
console.log(Object.getOwnPropertyDescriptors(square));

// arguments : {value: null, writable: false, enumerable: false, configurable: false}
// caller : {value: null, writable: false, enumerable: false, configurable: false}
// length : {value: 1, writable: false, enumerable: false, configurable: true}
// name : {value: 'square', writable: false, enumerable: false, configurable: true}
// prototype : {value: {…}, writable: true, enumerable: false, configurable: false}



// __proto__는 square 함수의 프로퍼티가 아니다.
console.log(Object.getOwnPropertyDescriptor(square, '__proto__')); // undefined

// __proto__는 Object.prototype 객체의 접근자 프로퍼티다.
// square 함수는 Object.prototype 객체로부터 __proto__ 접근자 프로퍼티를 상속받는다.
console.log(Object.getOwnPropertyDescriptor(Object.prototype,'__proto__'));
// {enumerable: false, configurable: true, get: ƒ, set: ƒ}
// configurable: trueenumerable: falseget: ƒ __proto__()set: ƒ __proto__()[[Prototype]]: Object

```

이처럼 arguments, caller, length, name, prototype 프로퍼티는 모두 함수 객체의 데이터 프로퍼티다. 이들 프로퍼티는 일반 객체에는 없는 함수 객체 고유의 프로퍼티다. 하지만 __proto__는 접근자 프로퍼티이며, 함수 객체 고유의 프로퍼티가 아니라 Object.prototype 객체의 프로퍼티를 상속받은 것을 알 수 있다.
<br>
Object.prototype객체의 프로퍼티는 모든 객체가 상속받아 사용할 수 있다. 즉, Object.prototype 객체의 __proto__ 접근자 프로퍼티는 모든 객체가 사용할 수 있다. 상속에 대해서는 19장 "프로포타입"에서 자세히 살펴보자.


### 18.2.1 arguments 프로퍼티

함수 객체의 arguments 프로퍼티 값은 arguments 객체다. arguments객체는 함수 호출 시 전달된 인수들의 정보를 담고 있는 순회 가능한 유사 배열 객체이며, 함수 내부에서 지역 변수처럼 사용된다. 즉, 함수 외부에서는 참조할 수 없다. <br>
함수 객체의 arguments프로퍼티는 현재 일부 브라우저에서 지원하고 있지만 ES3부터 표준에서 폐지되었다. 따라서 Function.arguments와 같은 사용법은 권장되지 않으며 함수 내부에서 지역변수처럼 사용할 수 있는 arguments객체를 참조하도록 한다.

```javascript

function multiply(x,y){
    console.log(arguments)
    return x * y;
}

// 함수 호출시 매개변수 개수만큼 인수를 전달하지 않아도 에러는 발생하지 않는다.
console.log(multiply()); // NaN
console.log(multiply(1)); // NaN
console.log(multiply(1,2)); // 2
console.log(multiply(1,2,3)); // 2

```
선언된 매개변수의 개수와 함수를 호출할 때 전달하는 인수의 개수를 확인하지 않는 자바스크립트의 특성 때문에 함수가 호출되면 인수 개수를 확인하고 이에 따라 함수의 동작을 달리 정의할 필요가 있을 수 있다. 이때 유용하게 사용하는 것이 arguments 객체다. <br>
arguments객체는 매개변수 개수를 확정할 수 없는 가변인자 함수를 사용할 때 유용하다.

``` javascript

function sum(){
    let res = 0;
    for(let i = 0; i <arguments.length; i++){
        res += arguments[i];
    }
    return res;
}

console.log(sum());
console.log(sum(1,2));
console.log(sum(1,2,3));

```

arguments 객체는 배열 형태로 인자 정보를 담고 있지만 실제 배열이 아닌 유사 배열 객체다. 유사배열 객체란 length프로퍼티를 가진 객체로 for문으로 순회할 수 있는 객체를 말한다.

> **유사배열 객체와 이터러블**<br>ES6에서 도입된 이터레셔널 프로토콜을 준수하면 순회 가능한 자료구조인 이터러블이 된다. 이터러블의 개념이 없었던 ES5에서 arguments객체는 유사 배열 객체로 구분되었다. 하지만 이터러블이 도입된 ES6부터 arguments객체는 유사배열 객체이면서 동시에 이터러블이다.

유사배열 객체는 배열이 아니므로 배열 메서드를 사용할 경우 에러가 발생한다. 따라서 배열 메서드를 사용하려면 Function.prototype.call, Function.prototype.apply를 사용해 간접 호출해야 하는 번거로움이 있다. 간접 호출과 배열에 대해서는 아직 살펴보지 않았으므로 참고만 하자.

```javascript

function sum(){0
    const array = Array.prototype.slice.call(arguments);
    return array.reduce(function(pre, cur){
        return pre + cur;
    }, 0);
}

console.log(sum(1,2)); // 3
console.log(sum(1,2,3,4,5)); // 15


// 이러한 번거로움을 해결하기 위해 ES6에서는 Rest 파라미터를 도입했다.
function sum (...args){
    return args.reduce((pre,cur) => pre + cur, 0);
}
console.log(sum(1,2)); // 3
console.log(sum(1,2,3,4,5)); // 15

```

Rest 의 도입으로 arguments객체의 중요성이 이전 같지는 않지만 언제나 ES6만 사용하지는 않을 수 있기 때문에 알아둘 필요가 있다. arguments객체와 Rest파라미터에 대해서는 26장에서 자세히 살펴볼 것이다.


### 18.2.2 caller 프로퍼티

caller 프로퍼티는 ECMAScript사양에 포함되지 않은 비표준 프로퍼티다. 이후 표준화될 예정도 없는 프로퍼티이므로 사용하지 말고 참고로 알아두자.<br>
caller프로퍼티는 함수 자신을 호출한 함수를 가리킨다.

``` javascript

function foo(func){
    return func();
}

function bar(){
    return 'caller : ' + bar.caller;
}

console.log(foo(bar)); // caller : function foo(func) {...}
console.log(bar()); // caller : null
``` 
함수 호출 foo(bar)의 경우 bar 함수를 foo 함수 내에서 호출했다. 이때 bar 함수의 caller프로퍼티는 bar함수를 호출한 foo함수를 가리킨다. 함수 호출 bar()의 경우 bar 함수를 호출한 함수는 없다. 따라서 caller프로퍼티는 null을 가리킨다.



### 18.2.3 length 프로퍼티

함수 객체의 length 프로퍼티는 **함수를 정의할 때 선언한 매개변수의 개수**를 가리킨다.

```javascript

function foo(){}
console.log(foo.length); // 0
    
function bar(x){
    return x;
}
console.log(bar.length); // 1

function baz(x,y){
    return x*y;
}
console.log(baz.length); // 2

```
arguments 객체의 length프로퍼티와 함수 객체의 length 프로퍼티의 값은 다를 수 있으므로 주의해야 한다. <br>
arguments 객체의 length프로퍼티는 인자의 개수를 가리키고, 함수 객체의 length프로퍼티는 매개변수의 개수를 가리킨다.

### 18.2.4 name 프로퍼티

함수 객체의 name 프로퍼티는 함수 이름을 나타낸다. name 프로퍼티는 ES6이전까지는 비표준이었다가 ES6에서 정식 표준이 되었다.

```javascript

// 기명 함수 표현식
var nameFunc = function foo() {};
console.log(nameFunc.name); // foo

// 익명 함수 표현식
var anonymousFunc = function () {};
// ES5 : name 프로퍼티는 빈 문자열을 값으로 갖는다.
// ES6 : name 프로퍼티는 함수 객체를 가리키는 변수 이름을 값으로 갖는다.
console.log(anonymousFunc.name); // anonymousFunc

// 함수 선언문
function bar() {};
console.log(bar.name); // bar

//함수를 호출할 때는 함수 이름이 아닌 함수 객체를 가리키는 식별자로 호출한다.

```

### 18.2.5 __proto__ 접근자 프로퍼티

모든 객체는 [[Prototype]]이라는 내부 슬롯을 갖는다. [[Prototype]]내부 슬롯은 객체지향 프로그래밍의 상속을 구현하는 프로토타입 객체를 가리킨다. <br>
__proto__프로퍼티는 [[Prototype]] 내부 슬롯이 가리키는 프로토타입 객체에 접근하기 위해 사용하는 접근자 프로퍼티다. 내부 슬롯에는 직접 접근할 수 없고 간접적인 접근 방법을 제공하는 경우에 한하여 접근할 수 있다.  [[Prototype]]내부 슬롯에도 직접 접근할 수 없으며 __proto__ 접근자 프로퍼티를 통해 간접적으로 프로토타입 객체에 접근할 수 있다.

```javascript

const obj = {a:1};

// 객체 리터럴 방식으로 생성한 객체의 프로토타입 객체는 Object.prototype이다.
console.log(obj.__proto__ === Object.prototype);// true

// 객체 리터럴 방식으로 생성한 객체는 프로토타입 객체인 Object.prototype의 프로퍼티를 상속받는다.
// hasOwnProperty메서드는 Object.prototype의 메서드다.
console.log(obj.hasOwnProperty('a')); // true
console.log(obj.hasOwnProperty('__proto__')); // false

```
> hasOwnProperty 메서드는 이름에서 알 수 있듯이 인수로 전달받은 프로퍼티 키가 객체 고유의 프로퍼티 키인 경우에만 true를 반환하고 상속받은 프로토타입의 프로퍼티 키인 경우 false를 반환한다.


### 18.2.6 prototype 프로퍼티

protoptype 프로퍼티는 생성자 함수로 호출할 수 있는 함수 객체, 즉 constructor만이 소유하는 프로퍼티다.
일반 객체와 생성자 함수로 호출할 수 없는 non-constructor에는 prototype 프로퍼티가 없다.<br>
prototype프로퍼티는 함수가 객체를 생성하는 생성자 함수로 호출될 때 생성자 함수가 생성할 인스턴스의 프로토타입 객체를 가리킨다.

```javascript

// 함수 객체는 prototype 프로퍼티를 소유한다.
(function(){}).hasOwnProperty('prototype'); // true

// 일반 객체는 prototype 프로퍼티를 소유하지 않는다.
({}).hasOwnProperty('prototype'); // false

```