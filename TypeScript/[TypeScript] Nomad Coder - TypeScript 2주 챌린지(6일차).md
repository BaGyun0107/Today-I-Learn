type에 특정값을 넣어서 지정해줄 수 있다.

```ts
type Team = "red" | "blue" | "yellow" // 타입에 특정값을 넣을 수 있다.
type Health = 1 | 5 | 10

interface Player {
  nickname: string,
  team:Team,
  health: Health
}

const nico : Player = {
  nickname: 'nico',
  team : "red", // 미리 지정해둔 특정값이 아닌 다른 값을 넣게되면 오류가 발생한다.
  health : 5
 }
```

### **interface?**

인터페이스는 오직 오브젝트의 모양을 특정해주는 용도만을 가지고 있다. (TypeScript에서만 사용)

React.js를 이용해 작업할 때 많이 사용된다.

또한, 인터페이스는 클래스 형태와 많이 닮아있다.

```ts
interface User {
  name: string
}

interface Player extends User { // 클래스 형식처럼 상속시키는 형태
}

const nico : Player = {
  name: "nico"
}

// 인터페이스의 또 다른 특징으로 property들을 축적시킬 수 있다.
interface User {
  name: string
}

interface User {
  lastName: string
}

interface User {
  health: number
}

const nico: User = { // 이런식으로 축적된 property를 입력할 수 있다.
  name: "nico",
  lastName: "n",
  health: 10
}
```

추상 클래스는 JS로 컴파일시 일반 클래스로 남는 반면, interface는 컴파일시 사라진다  
  
즉, 추상 클래스를 interface로 대체할 수 있다면 JS 코드가 더 가벼워진다!

```ts
abstract class User {
    constructor(
        protected firstName: string,
        protected lastName: string
    ) {}
    abstract sayHi(name: string): string
    abstract fullName(): string
}

class Player extends User {
    fullName() {
        return `${this.firstName} ${this.lastName}`;
    }
    sayHi(name: string) {
        return `Hello ${name}. My name is ${this.fullName()}`;
    }
}

// 위와 같은 추상 클래스를 interface로 대체해보자
interface User {
    firstName: string,
    lastName: string,
    sayHi(name: string): string,
    fullName(): string
}

class Player implements User { // 클래스가 interface를 implements로 상속받을 수 있다.
    constructor(
        public firstName: string, // public의 형태로만 사용 가능 protected, private는 사용 불가능
        public lastName: string,
    ) {}
    fullName() {
        return `${this.firstName} ${this.lastName}`;
    }
    sayHi(name: string) {
        return `Hello ${name}. My name is ${this.fullName()}`;
    }
}


function makeUser (user: User){
    console.log(user);
}

makeUser({ // 인터페이스의 형태와 동일하게 넣어주면 된다.
    firstName: "kim",
    lastName: "sungjoong",
    fullName: () => "full name",
    sayHi: (name) => `hi ${name}`
});
```
