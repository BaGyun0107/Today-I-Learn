## **Call Signatures**

함수에 대한 타입을 만들 수 있고, 함수가 어떻게 작동하는 지 서술할 수 있다.

즉, `함수의 인자(arguments)의 타입과 함수의 반환 타입을 정해줄 수 있다.`

```
type Add = (a:number, b: number) => number // 이러한 형식을 call signatures 라고 불림

const add:Add = (a,b) => a+b
```

## **Overloading**

오버로딩은 함수가 여러개의 Call Signatures를 가지고 있을 때 발생시킨다.

예시1.

```
type Config = {
  path: string,
  state: object
}

type Push = {
  (path: string): void
  (config: Config): void
}

const push:Push = (config) => {
  if(typeof config === "string") { console.log(config) } // config의 타입을 stirng 지정
  else { 
    console.log(config.path, config.state) // type Config의 객체를 가지고 올 수 있다.
  }
}
```

예시2.

```
type Add = {
  (a: number, b:number) : number,
  (a: number, b:number, c:number): number
}

const add : Add = (a, b, c?:number) => { //c를 optional하게 사용할 수 있다.
  if(c) return a+b+c
  return a+b
}

const add : Add = (a, b, c) => { // 이 함수는 c 타입을 지정해주지 않았기 때문에 에러가 발생한다.
  return a+b
}
```
