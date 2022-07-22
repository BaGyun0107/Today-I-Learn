## **06장. 데이터 타입**

자바스크립트의 모든 값은 데이터 타입을 갖는다. 자바스크립트(ES6)는 7개의 데이터 타입을 제공한다.

7개의 데이터 타입은`원시 타입(primitive type)`과 `객체 타입(object/reference type)`으로 분류할 수 있다.

| **구분** | **데이터 타입** | **설명** |
| --- | --- | --- |
| 원시 타입 | 숫자(number) 타입 | 숫자, 정수와 실수 구분 없이 하나의 숫자 타입만 존재 |
| |문자열(string) 타입 | 문자열 |
| |불리언(boolean) 타입 | 논리적 참(true)과 거짓(false) |
| |undefined 타입 | var 키워드로 선언된 변수에 암묵적으로 할당되는 값 |
| |null 타입 | 값이 없다는 것을 의도적으로 명시할 때 사용하는 값 |
| |심벌(symbol) 타입 | ES6에서 추가된 7번째 타입 |
| 객체타입 || 객체, 함수, 배열 등 |

### **6.1 숫자 타입**

자바스크립트의 숫자 타입은 정수만을 위한 타입이 없고 모든 수를 실수로 처리한다. 이는 정수로 표시된다 해도 사실은 실수라는 것을 의미한다. 따라서 정수로 표시되는 수끼리 나누더라도 실수가 나올 수 있다.

```js
// 숫자 타입은 모두 실수로 처리된다.
console.log(1 === 1.0); // true
console.log(4 / 2); // 2
console.log(3 / 2); // 1.5
```

숫자 타입은 추가적으로 세 가지 특별한 값도 표현할 수 있다.

-   Infinity: 양의 무한대
-   \-Infinity: 음의 무한대
-   NaN: 산술 연산 불가(not-a-number)

```js
// 숫자 타입의 세 가지 특별한 값
console.log(10 / 0); // Infinity
console.log(10 / -0); // -Infinity
console.log(1 * 'String'); // NaN
```

자바스크립트는 대소문자를 구별(case-sensitive)하므로 NaN을 NAN, Nan, nan과 같이 표현하면 에러가 발생하므로 주의하기 바란다.

### **6.2 문자열 타입**

문자열(string) 타입은 텍스트 데이터를 나타내는 데 사용한다. 문자열은 0개 이상의 16비트 유니코드 문자(UTF-16)의 집합으로 전 세계 대부분의 문자를 표현할 수 있다.

`문자열은 작은따옴표(' '), 큰따옴표(" "),또는 백틱(``)으로 텍스트를 감싼다`. 자바스크립트에서 가장 일반적인 표기법은 작은따옴표를 사용하는 것이다.

```js
var string;
string = '문자열'; // 작은따옴표
string = "문자열"; // 큰따옴표
string = `문자열`; // 백틱(ES6)

string = '작은따옴표로 감싼 문자열 내의 "큰따옴표"는 문자열로 인식된다.';
string = "큰따옴표로 감싼 문자열 내의 '작은따옴표'는 문자열로 인식된다.";
```

다른 타입의 값과 달리 문자열을 따옴표로 감싸는 이뉴는 키워드나 식별자 같은 토큰과 구분하기 위해서다. 만약 문자열을 따옴표로 감싸지 않으면 자바스크립트 엔진은 키워드나 식별자 같은 토큰으로 인식한다.

### **6.3 템플릿 리터럴**

`ES6부터 템플릿 리터럴(template literal)이라고 하는 새로운 만자열 표기법이 도입되었다.` 템플릿 리터럴은 멀티라인 문자열(multi-line string), 표현식 삽입(expression interpolation), 태그드 템플릿(tagged template) 등 편리한 문자열 처리 기능을 제공한다. 템플릿 리터럴은 런타임에 일반 문자열로 변환되어 처리된다.

템플릿 리터럴은 일반 문자열과 비슷해 보이지만 작은따옴표(' ') 또는 큰따옴표(" ") 같은 일반적인 따옴표 대신 백틱(\`\`)을 사용해 표현한다.

#### **6.3.1 멀티라인 문자열**

일반 문자열 내에서는 줄바꿈(개행)이 허용되지 않는다.

```js
var str = "hello
world" ;
// SyntaxError: Invalid or unexpected token
```

따라서 일반 문자열 내에서 줄바꿈 등의 공백(white space)을 표현하려면 백슬래시(\\)로 시작하는 이스케이프 시퀀스(escape sequence)를 사용해야 한다.

이스케이프 시퀀스의미

| **이스케이프 시퀀스** | **의미** |
| --- | --- |
| \\0 | Null |
| \\b | 백스페이스 |
| \\f | 폼 피드(Form Feed): 프린터로 출력할 경우 다음 페이지의 시작 지점으로 이동 |
| \\n | 개행(LF, Line Feed): 다음 행으로 이동 |
| \\r | 개행(CR, Carriage Return): 커서를 처음으로 이동 |
| \\t | 탭(수평) |
| \\v | 탭(수직) |
| \\uXXXX | 유니코드. 예를 들어 '\\u0041'은 'A' |
| \\' | 작은따옴표 |
| \\" | 큰따옴표 |
| \\\\ | 백슬래시 |

```js
// 일반 문자열 표기시 ("", '')
var template = '<ul>\n\t<li><a href="#">Home</a></li>\n</ul>'

console.log(template);
// 출력 결과
<ul>
  <li><a href="#">Home</a></li>
</ul>

// 템플릿 리터럴 표기 시 (백틱(`))
var template = `<ul>
<li><a href="#">Home</a></li>
</ul>`

console.log(template);
// 출력 결과
<ul>
  <li><a href="#">Home</a></li>
</ul>
```

#### **6.3.2 표현식 삽입**

`문자열은 문자열 연산자 +를 사용해 연결할 수 있다.` + 연산자는 피연산자 중 하나 이상이 문자열인 경우 문자열 연결 연산자로 동작한다.

```js
var first = 'Ung-mo';
var last = 'Lee';

// ES5: 문자열 연결
console.log('My name is ' + first + ' ' + last + '.');
// My name is Ung-mo Lee.
```

탬플릿 리터럴 내에서는 표현식 삽입(expression interpolation)을 통해 간단히 문자열을 삽입할 수 있다.

```js
var first = 'Ung-mo';
var last = 'Lee';

// ES6: 표현식 삽입
console.log(`My name is ${first} ${last}.`);
// My name is Ung-mo Lee.
```

`표현식을 삽입하려면 ${}으로 표현식을 감싼다.` 이때 표현식의 평가 결과가 문자열이 아니더라도 문자열로 타입이 강제로 변환되어 삽입된다.

### **6.4 불리언 타입**

`불리언 타입의 값은 논리적 참, 거짓을 나타내는 true와 false뿐이다`

```js
var foo = true;
console.log(foo); // true

foo = false;
console.log(foo); // false
```

### **6.5 undefined 타입**

undefined 타입의 값은 undefined가 유일하다.

undefined는 개발자가 의도적으로 할당하기 위한 값이 아니라 자바스크립트 엔진이 변수를 초기화 할 때 사용하는 값이다.

변수를 참조했을 때 undefined가 변환된다면 참조한 변수가 선언 이후 값이 할당된적이 없는, 즉 초기화되지 않은 변수라는 것을 간파할 수 있다.

```js
var foo;
console.log(foo); // undefined
```

undefined는 자바스크립트 엔진이 변수를 초기화하는 데 사용하기 때문에 개발자가 의도적으로 변수에 할당하는 건 본래의 취지와 어긋나므로 권장되지 않는다.  
`따라서, 변수에 값이 없다는 것을 명시하고자 할때는 null을 할당한다.`

### **6.6 null 타입**

null 타입의 값은 null이 유일하다. 자바스크립트는 대소문자를 구별하므로 null은 Null, NULL 등과 다르다.

프로그래밍 언어에서 null은 변수에값이 없다는 것을 의도적으로 명시(의도적 부재(intentional absence))할 때 사용한다.

함수가 유효한 값을 반환할 수 없는 경우 명시적으로 null을 반환하기도 한다.

```js
var foo = 'Lee';
// 이전 참조를 제거. foo 변수는 더 이상 'Lee'를 참조하지 않는다.
// 유용해 보이지는 않는다. 변수의 스코프를 좁게 만들어 변수 자체를 재빨리 소멸시는 편이 낫다.
foo = null;

<!DOCTYPE html>
<html>
<body>
  <script>
    var element = document.querySelector('.myClass');
    
    // HTML 문서에 myClass 클래스를 갖는 요소가 없다면 null을 반환한다.
    console.log(elemnet); // null
  </script>
</body>
</html>
```

### **6.7 심벌 타입**

`심벌(symbol)은 ES6에서 추가된 7번째 타입으로, 변경 불가능한 원시 타입의 값`이다.

심벌 값은 다른 값과 중복되지 안흔 유일무이한 값이다. 따라서 주로 이름이 충돌할 위험이 없는 유일한 프로퍼티 키를 만들기 위해 사용한다.

```js
// 심벌 값 생성
var key = Symbol('key');
console.log(typeof key); //symbol

// 객체 생성
var obj = {};

// 이름이 충돌할 위험이 없는 유일무이한 값인 심벌을 프로퍼티 키로 사용한다.
obj[key] = 'value';
console.log(obj[key]); // value
```

### **6.8 데이터 타입의 필요성**

데이터 타입은 값의 종류를 말한다. 자바스크립트의 모든 값은 데이터 타입을 갖는다. 데이터 타입이 필요한 이유는 다음과 같다.

-   값을 저장할 때 확보해야 하는 `메모리 공간의 크기`를 결정하기 위해
-   값을 참조할 때 한 번에 읽어 들여야 할 `메모리 공간의 크기`를 결정하기 위해
-   메모리에서 읽어 들인 `2진수를 어떻게 해석할지` 결정하기 위해

### **6.9 동적 타이핑**

#### **6.9.1 동적 타입 언어와 정적 타입 언어**

C나 자바 같은 `정적 타입(static/strong type)언어`는 변수를 선언할 때 변수에 할당할 수 있는 값의 종류, 즉 데이터 타입을 사전에 선언해야 한다.

이를 `명시적 타입 선언(explicit type declaration)`이라 한다.

```js
// c 변수에는 1바이트 정수 타입의 값(-128 ~ 127)만 할당할 수 있다.
char C;

// num 변수에는 4바이트 정수 타입의 값(-2,124,483,648 ~ 2,124,483,647) 만 할당할 수 있다.
int num;
```

`정적 타입 언어는 컴파일 시점에 타입 체크(선언한 데이터 타입에 맞는 값을 할당했는지 검사하는 처리)를 수행한다.`

이를 통해 타입의 일관성을 강제함으로써 더욱 안정적인 코드의 구현을 통해 런타임에 발생하는 에러를 줄인다. 대표적인 정적 타입 언어로 C, C++, 자바(Java), 코틀린(Kotlin), 고(Go), 하스켈(Haskell), 러스트(Rust), 스칼라(Scala) 등이 있다.

`자바스크립트는 정적 타입 언어와 다르게 변수를 선언할 때 타입을 선언하지 않는다.` 다만 var, let, const 키워드를 사용해 변수를 선언할 뿐이다. 변수를 하나 선언하고 지금까지 살펴본 다양한 데이터 타입의 값을 할당한 다음, typeof 연산자로 변수의 데이터 타입을 조사해 보자.

```js
var foo;
console.log(typeof foo); // undefined

foo = 3;
console.log(typeof foo); // number

foo = 'Hello';
console.log(typeof foo); // string

foo = true;
console.log(typeof foo); // boolean

foo = null;
console.log(typeof foo); // object

foo = Symbol(); // 심벌
console.log(typeof foo); // symbol

foo = {}; // 객체
console.log(typeof foo); // object

foo = []; // 배열
console.log(typeof foo); // object

foo = function () {}; // 함수
console.log(typeof foo); // function
```

`자바스크립트의 변수는 선언이 아닌 할당에 의해 타입이 결정(타입 추론(type inference))된다. 그리고 재할당에 의해 변수의 타입은 언제든지 동적으로 변할 수 있다.` 이러한 특징을 `동적 타이핑(dynamic typing)`이라 하며, 자바스크립트를 정적 타입 언어와 구별하기 위해 `동적 타입(dynamic/weak type)언어`라 한다. 대표적인 동적 타입 언어로는 자바스크립트, 파이썬(Python), PHP, 루비(Ruby), 리스프(Lisp), 펄(Perl) 등이 있다.
