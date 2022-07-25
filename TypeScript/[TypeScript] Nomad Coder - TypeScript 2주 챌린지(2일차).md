## **타입스크립트의 타입들**

우선 object의 타입을 정의해줄 때, 선택적 변수를 지정하는 방법은 아래 예시와 같다.

```ts
const player : {
  name: string,
  age?: number, // optional하게 사용하고 싶은 값에 ?를 붙여준다.
} = {
  name: "nico",
}

age의 경우 number | undefined 값을 주어주는데

if (player.age && player.age<10) { // player.age는 number 타입이라는 것을 명시함으로써 선택적 변수(optional parameter)를 지정해준다.

}
```

### **Alias Type**

object에서 타입을 지정해줄 때, 여러 변수에 반복적으로 타입을 지정해줘야하는 경우 Alias(별칭) Type을 만들어준다.

```ts
// 첫글자는 대문자
type Name = string;
type Age = number;
type Player = {      type Player = { // 왼쪽과 오른쪽은 동일하다. 
  name: Name,           name: string,  // 이런 식으로 Alias 타입을 지정해줄 수 있다는 것을 보여주기 위함
  age?: Age             age?: number,  // 코드가 깔끔하고 명확해질 때까지만 이렇게 작업을 하면 된다.
}                     }
```

위 예시처럼, Alias 타입을 만들어서 여러 변수에 재사용할 수 있게끔 만들어 주는 것이다.

```ts
type Age = number;
type Name = string;
type Player = {
  name: Name,
  age?: Age
}

function playerMaker(name:string) : Player { // 미리 만든 Alias 타입으로 지정해준다
  return {
    name: name,   // name 만 적어도 무관하다.
  }
}

//화살표 함수로 표현하는 법
const playerMaker = (name:string) : Player => ({name})

const nico = playerMaker("nico")
nico.age = 12 // optional한 값을 지정해줄 수 있다.
```

### **readonly 속성**

readonly 속성은 요소들을 '읽기 전용'으로 만들어 주는 것이다. JavaScript에서는 없는 동작으로 TypeScript에서만 사용 가능하다.

TypeScript의 보호장치가 있기 때문에 가능한 것이며, immutability(불변성)을 가지게 만든다.

```ts
type Age = number;
type Name = string;
type Player = {
  readonly name: Name,
  age?: Age
}

function playerMaker(name:string) : Player {
  return {
    name
  }
}

const nico = playerMaker("nico")
nico.age = 12
nico.name = "las" // 오류가 발생한다. type Player에 readonly 속성을 넣어줌으로써, 수정이 불가하게끔 만들어준다.
```

### **Tuple Type**

Tuple은 배열을 최소한의 길이를 가지게 하고 특정 위치에 특정 타입이 있게끔 만들어준다.

```ts
const player: [string, number, boolean] = ["nico", 1, true]
// player의 배열은 3개의 아이템을 가지게하고, string, number, boolean 순서대로여야 함을 알린다.

const player: readonly [string, number, boolean] = ["nico", 1, true]
// 이렇게 readonly의 속성도 사용할 수 있다.
```

### **any Type**

any는 TypeScript의 보호 장치에서 벗어날 수 있게 해준다. 즉 JavaScript에서 사용했던거처럼 모든 것을 허용해준다는 의미

```ts
const a : any[] = [1, 2, 3, 4]
const b : any = true

a + b // '1,2,3,4true'

// 타입스크립트에서 자바스크립트처럼 작동한다.
```

자주 사용하는 것은 좋지 않으나, 탈출구가 존재한다는 것을 알고 있는 것이 좋다.

### **unknown Type**

어떤 타입인지 모르는 변수는 TypeScript에게 어떻게 말해줘야 할까? 라는 의문이 생길 때 unknown을 붙여주면 된다.

```ts
let a: unknown;

if (typeof a === 'number') { // 이러한 조건문을 통해 a의 타입을 정해줌
  let b = a + 1
}
if (typeof a === 'string') {
  let b = a.toUpperCase();
}
```

### **void Type**

아무것도 return 하지 않는 함수를 대상으로 사용한다.

보통 void를 따로 지정해줄 필요는 없다. TypeScript가 이 함수는 아무것도 return하지 않는다는 것을 자동으로 인식한다.

```ts
function hello() {
  console.log('x')
}
```

### **never Type**

많이 사용하진 않지만 never는 함수가 절대 retrun 하지 않을 때 발생한다.

함수에서 exception(예외)이 발생할 때 또는 타입이 두가지 일 수도 있는 상황에 발생할 수 있다.

```ts
function hello (): never {
  throw new Error("xxx")
}

function hello (name:string|number) {
  if (typeof name === "string") {
    name // string Type
  } else if (typeof name === "number") {
    name // number Type
  } else {
    name // never Type 절대 실행되면 안된다는걸 나타냄
  }
}
```
