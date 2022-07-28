## **09장. 타입 변환과 단축 평가**

### **9.1 타입 변환이란?**

개발자가 의도적으로 값의 타입을 변환하는 것을 `명시적 타입 변환(explicit coercion)` 또는 `타입 캐스팅(type casting)`이라 한다.

```js
let x = 10;

// 명시적 타입 변환
// 숫자를 문자로 타입 캐스팅한다.
let str = x.toString();
console.log(typeof str, str); // string 10

// 값의 타입만 변할 뿐 값은 동일하다
console.log(typeof x, x); // number 10
```

개발자의 의도와는 상관없이 표현식을 평가하는 도중에 자바스크립트 엔진에 의해 암묵적으로 타입이 자동 변환되기도 한다. 이를 `암묵적 타입 변환(implicit coercion)` 또는 `타입 강제 변환(type coercion)`이라 한다.

```js
let x = 10;

// 암묵적 타입 변환
// 문자열 연결 연산자는 숫자 타입 x의 값을 바탕으로 새로운 문자열을 생성한다.
let str = 10 + '';
console.log(typeof str, str) // string 10

// x 변수의 값이 변경된 것은 아니다.
console.log(typeof x, x) // number 10
```

### **9.2 암묵적 타입 변환**

자바스크립트 엔진은 표현식을 평가할 때 개발자의 의도와는 상관없이 코드의 문맥을 고려해 암묵적으로 데이터 타입을 강제 변환(암묵적 타입 변환)할 때가 있다.

#### **9.2.1 문자열 타입으로 변환**

\+ 연산자는 피연산자 중 하나 이상이 문자열이면 문자열 연결 연산자로 동작한다.

```js
// 숫자 타입 
0 + ''  // '0'
-0 + '' // '0'
1 + '' // '1'
-1 + '' // '-1'
NaN + '' // 'NaN'
Infinity + '' // 'Infinity'
-Infinity + '' // '-Infinity'

// 불리언 타입
true + '' // 'true'
false + '' // 'false'

// null 타입
null + '' // 'null'

//undefined 타입
undefined + '' // 'undefined'

// 심벌 타입
(Symbol()) + '' // -> TypeError: Cannot convert a Symbol value to a string

// 객체 타입
({}) + '' // '[object Object]'
Math + '' // '[object Math]'
[] + '' // ''
[10, 20] + '' // '10,20'
(function(){}) + '' // 'function(){}'
Array + '' // 'function Array(){ [native code] }'
```

#### **9.2.2 숫자 타입으로 변환**

산술 연산자의 역할은 숫자 값을 만드는 것이다. 따라서 산술 연산자의 모든 피연산자는 코드 문맥상 모두 숫자 타입어야 한다. 자바스크립트 엔진은 비교 연산자 표현식을 평가하기 위해 비교 연산자의 피연산자 중에서 숫자 타입이 아닌 피연산자를 숫자 타입으로 암묵적 타입 변환한다.

```js
// 문자열 타입
+'' // 0
+'0' // 0
+'1' // 1
+'string' // NaN

// 불리언 타입
+true // 1
+false // 0

// null 타입
+null // 0

// undefined 타입
+undefined // NaN

// 심벌 타입
+Symbol() // TypeError : Cannnot convert a Symbol value to a number

// 객체 타입
+{} // NaN
+[] // 0
+[10, 20] // NaN
+(function(){}) // NaN
```

#### **9.2.3 불리언 타입으로 변환**

if 문이나 for 문과 같은 제어문 또는 삼항 조건 연산자의 조건식은 불리언 값, 즉 논리적참/거짓으로 평가되어야 하는 표현식이다. 자바스크립트 엔진은 조건식의 평가 결과를 불리언 타입으로 암묵적 타입 변환한다.

이때, `자바스크립트 엔진은 불리언 타입이 아닌 값을 Truthy 값(참으로 평가되는 값) 또는 falsy 값(거짓으로 평가되는 값)으로 구분한다.`

-   false
-   undefined
-   null
-   0, -0
-   NaN
-   ' '(빈 문자열)

### **9.3 명시적 타입 변환**

표준 빌트인 생성자 함수(String, Number, Boolean)를 new 연산자 없이 호출하는 방법과 빌트인 메서드를 사용하는 방법, 그리고 앞에서 살펴본 암묵적 타입 변환을 이용하는 방법이 있다.

#### **9.3.1 문자열 타입으로 변환**

문자열 타입이 아닌 값을 문자열 타입으로 변환하는 방법은 다음과 같다.

1\. String 생성자 함수를 new 연산자 없이 호출하는 방법

```js
// 숫자 타입 => 문자열 타입
String(1); // '1'
String(NaN); // 'NaN'
String(Infinity); // 'Infinity'

// 불리언 타입 => 문자열 타입
String(true); // 'true'
String(false); // 'false'
```

2.Object.prototype.toString 메서드를 사용하는 방법

```js
// 숫자 타입 => 문자열 타입
(1).toString() // '1'
(NaN).toString() // 'NaN'
(Infinity).toString() // 'Infinity'

// 불리언 타입 => 문자열 타입
(true).toString() // 'true'
(false).toString() // 'false'
```

3\. 문자열 연결 연산자를 이용하는 방법

```js
// 숫자 타입 => 문자열 타입
1 + '' // '1'
NaN + '' // 'NaN'
Infinity + '' // 'Infinity'

// 불리언 타입 => 문자열 타입
true + '' // 'true'
false + '' // 'false'
```

#### **9.3.2 숫자 타입으로 변환**

숫자 타입이 아닌 값을 숫자 타입으로 변환하는 방법은 다음과 같다.

1.Number 생성자 함수를 new 연산자 없이 호출하는 방법

```js
// 문자열 타입 => 숫자 타입
Number('0'); // 0
Number('-1'); // -1
Number('10.53'); // 10.53

// 불리언 타입 => 숫자 타입
Number(true); // 1
Number(false); // 0
```

2.parseInt, parseFloat 함수를 사용하는 방법(문자열만 변환 가능)

```js
// 문자열 타입 => 숫자 타입
ParseInt('0'); // 0
ParseInt('-1'); // -1
ParseFloat('10.53'); // 10.53
```

3\. + 단항 산술 연산자를 이용하는 방법

```js
// 문자열 타입 => 숫자 타입
+'0'; // 0
+'-1'; // -1
+'10.53'; // 10.53

// 불리언 타입 => 숫자 타입
+true; // 1
+false; // 0
```

4\. \* 산술 연산자를 이용하는 방법

```js
// 문자열 타입 => 숫자 타입
'0' * 1; // 0
'-1' * 1; // -1
'10.53' * 1; // 10.53

// 불리언 타입 => 숫자 타입
true * 1; // 1
false * 1 // 0
```

#### **9.3.3 불리언 타입으로 변환**

불리언 타입이 아닌 값을 불리언 타입으로 변환하는 방법은 다음과 같다.

1\. Boolean 생성자 함수를 new 연산자 없이 호출하는 방법

```js
// 문자열 타입 => 불리언 타입
Boolean('x'); // true
Boolean(''); // false
Boolean('false'); // true

// 숫자 타입 => 불리언 타입
Boolean(0); // false
Boolean(1); // true
Boolean(NaN); // false
Boolean(Infinity); // true

// null 타입 => 불리언 타입
Boolean(null); // true

// undefined 타입 => 불리언 타입
Boolean(undefiend); // false

// 객체 타입 => 불리언 타입
Boolean({}) //true
Boolean([]) // true
```

2\. ! 부정 논리 연산자를 두 번 사용하는 방법

```js
// 문자열 타입 => 불리언 타입
!!'x'; // true
!!''; // false
!!'false'; // true

// 숫자 타입 => 불리언 타입
!!0; // false
!!1; // true
!!NaN; // false
!!Infinity; // true

// null 타입 => 불리언 타입
!!null; // false

// undefined 타입 => 불리언 타입
!!undefined; // false

// 객체 타입 => 불리언 타입
!!{}; // true
!![]; // true
```

### **9.4 단축 평가**

#### **9.4.1 논리 연산자를 사용한 단축 평가**

논리곱(&&) 연산자와 논리합(||) 연산자는 `논리 연산의 결과를 결정하는 피연산자를 타입 변환하지 않고 그대로 반환한다. 이를 단축 평가(short-circuit evaluation)라 한다. 단축 평가는 표현식을 평가하는 도중에 평가 결과가 확정된 경우 나머지 평가 과정을 생략하는 것을 말한다.`

| **단축 평가 표현식** | **평가 결과** |
| --- | --- |
| true \|\| anything | true |
| false \|\| anything | anything |
| true && anything | anything |
| false && anything | false |

```js
// 논리합(||) 연산자 예시
'Cat' || 'Dog' // 'Cat'
false || 'Dog' // 'Dog'
'Cat' || false // 'Cat'

// 논리곱(&&) 연산자 예시
'Cat' && 'Dog' // 'Dog'
false && 'Dog' // false
'Cat' && false // false
```

#### **9.4.2 옵셔널 체이닝 연산자**

ES11(ECMAScript2020)에서 도입된 옵셔널 체이닝(optional chaining) 연산자 ?.는 좌항의 피연산자가 null 또는 undefined인 경우 undefined를 반환하고, 그렇지 않으면 우항의 프로퍼티 참조를 이어간다.

```js
var elem = null;

// elem이 null 또는 undefined이면 undefined를 반환하고, 그렇지 않으면 우항의 프로퍼티 참조를 이어간다.
var value = elem?.value;
console.log(value); // undefined
```

#### **9.4.3 null 병합 연산자**

ES11(ECMAScript2020)에서 도입된 null 병합(nullish coalescing)연산자 ?? 는 좌항의 피연산자가 null 또는 undefined인 경우 우항의 피연산자를 반환하고, 그렇지 않으면 좌항의 피연산자를 반환한다. null 병합 연산자 ??는 변수에 기본값을 설정할 때 유용하다.

```js
// 좌항의 피연산자가 null 또는 undefined이면 우항의 피연산자를 반환하고,
// 그렇지 않으면 좌항의 피연산자를 반환한다.
var foo = null ?? 'default string';
console.log(foo); 'default string'
```
