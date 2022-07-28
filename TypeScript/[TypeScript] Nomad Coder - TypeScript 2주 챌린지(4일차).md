### **다형성(polymorphism)**

poly = many, several, much, multy를 의미

morphos, morphic = form, structure를 의미

이것을 합쳐서 polymorphism은 여러가지 다른 구조들, 여러가지 다른 형태들이란 의미다.

```js
type SuperPrint = {
  (arr : number[]) : void
  (arr : boolean[]) : void
  (arr : string[]) : void
}

const superPrint : SuperPrint = (arr) => {
  arr.forEach(i => console.log(i))
}

superPrint([1, 2, 3, 4])  
superPrint([true, false, true])
superPrint(["a", "b", "c"])

superPrint([1, 2, true, false]) // 이 배열은 오류가 발생한다 왜? call signature에 미리 타입을 지정해주지 않았기 때문
```

위 예시처럼 만약 call signature에 들어올 확실한 타입을 모른다면 모든 가능성을 다 조합해서 만들어야할 것이다.

함수에 확실한 타입을 모를 경우 call signature 작성할 때, generic type을 사용한다.

generic을 사용하다보면, call signature에 모든 가능성을 다 조합할바에 any를 넣으면 되지않을까란 생각을 할 수도 있는데, generic과 any는 엄연히 다르다. generic은 요구에 따라 call signature를 생성하는 방식이다.

### **generic Type?**

타입스크립트가 타입을 유추한다.

concrete type을 사용하는 것 대신 쓸 수 있다.

### **concrete type?**

우리가 전부터 봐왔던 타입을 말한다

ex)string, number, boolean, void, unknown 등등

generic 타입을 사용하기 위해선,

1.  타입스크립트한테 generic 타입을 사용한다고 알려준다.
2.  call signature에 '<>'괄호를 열어서 안에 임의의 이름을 넣어준다

```js
type SuperPrint = {
  <T>(arr : T[]) : void // 이 형태를 generic type 이라고 칭한다.
}

const superPrint : SuperPrint = (arr) => {
  arr.forEach(i => console.log(i))
}

// 타입스크립트는 값들을 보고 타입을 유추하고, 유추한 타입으로 call signature를 우리에게 보여준다.
superPrint([1, 2, 3, 4])  // const superPrint: <number>(arr: number[]) => void
superPrint([true, false, true]) // const superPrint: <boolean>(arr: boolean[]) => void
superPrint(["a", "b", "c"]) // const superPrint: <string>(arr: string[]) => void
```

이러한 특징을 응용해서

```js
type SuperPrint = {
  <T>(arr : T[]) : T
}

const superPrint : SuperPrint = (arr) => arr[0]

superPrint([1, 2, 3, 4])  // 1
superPrint([true, false, true]) // true
superPrint(["a", "b", "c"]) // "a"
```

배열에 첫 번째 요소를 리턴하는 함수를 만들 수 있다.

만약 SuperPrint타입에 generic을 더 추가하고 싶다고 가정했을 땐

```js
type SuperPrint = {
  <T, M>(a : T[], b:M) : T // 2개의 인자(arguments)를 넣어줄 수 있다.
}

const superPrint : SuperPrint = (arr) => arr[0]

superPrint([1, 2, 3, 4] , "X") // 2개의 인자(arguments)를 예상하고 있으니 2개를 넣어줘야 오류발생하지 않는다.
superPrint([true, false, true], 1)
superPrint(["a", "b", "c"], true)
```

여태까지의 예시처럼 generic을 사용해서 직접 call signature를 만드는 경우는 거의 드물다.

라이브러리를 만들거나, 다른 개발자가 사용할 기능을 개발하는 경우엔 예시처럼 사용하는 generic이 유용할 것이다.

다른 generic의 사용법 예시를 보면,

```js
type Player<E> = { // 예시로 여러개의 타입이 들어있는 큰 타입
  name: string
  extraInfo: E
}

const nico: Player<{favFood: string}> = { // extraInfo를 object 타입으로 넣어주는 예시
  name: "nico",
  extraInfo: {
    favFood:"kimchi"
  }
}

const lynn: Player<null> = { // extraInfo를 null 타입으로 넣어주는 예시
  name: lynn,
  extraInfo: null
}
```

예를 들어 여러개의 타입이 들어있는 큰 타입을 하나 가지고 있는데, 그 중 하나가 달라질 수 있는 타입이라면 generic을 넣으면 된다.

generic은 함수에서만 사용될 뿐만아니라 여러곳에서 사용이 된다.

```js
type A = Array<number> // number[] 이랑 동일한 의미, 하지만 이런 방식의 코드를 더 많이 보게 될 것이다.

let a:A = [1, 2, 3, 4]

function printAllNumbers(arr: Array<number>){} // 함수 역시 마찬가지로 number[]랑 동일한 의미

// Reactjs에서 useState에도 사용이 된다
useState<number>()
```
