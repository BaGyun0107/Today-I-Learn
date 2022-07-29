### **TypeScript로 객체지향 프로그래밍하기**

```ts
abstract class User { // 추상 클래스
  constructor (
    protected firstName:string, // protected, private, public의 차이를 잘 이해하자
    private lastName:string,
    public nickname:string
  ) {}
  abstract getNickName():void // 추상 메소드 call signature만 가지고 있다

  getFullName(){ // 메소드에도 protected, private, public을 넣어줄 수 있다. 안적었다면, public 상태
    return `${this.firstName} ${this.lastName}`
  }
}

class Player extends User {
  getNickName() { // 추상 클래스를 상속 받았을 때, 추상 메소드가 있다면 꼭 구현 해줘야 한다.
    console.log(this.firstName)
  }
}

const nico = new Player("nico", "las", "니꼬")

nico.getFullName() // nico는 User를 상속 받았기때문에 class 내부의 메소드 사용 가능
```
<div align ="center">
  
| **접근 가능성** | **public** | **protected** | **private** |
| --- | --- | --- | --- |
| 클래스 내부 | O | O | O |
| 자식 클래스 내부 | O | O | X |
| 클래스 인스턴스 | O | X | X |
  
</div>
abstract 클래스는 오직 다른곳에서 상속받을수만 있고, 직접적으로 인스턴스를 만들지는 못하는 클래스라  
위 예시의 abstract 클래스인 \`User로 new User("nico", "las", "니꼬")\`로 인스턴스를 만들 수 없다  
  
protected, private, public은 따로 작성해주지 않으면 public 상태가 된다.

```ts
type Words = {
  [key: string]: string
}

class Dict {
  private words: Words
  constructor() {
    this.words = {}
  }
  add(word: Word) { // class Word를 타입처럼 사용이 가능
    if (this.words[word.term] === undefined) {
       this.words[word.term] = word.def;
    }
  }
  def(term:string){ // 조회 메소드
    return this.words[term]
  }
}

class Word {
  constructor(
    public term: string,
    public def: string
  ) {}
}

const kimchi = new Word("kimchi", "한국의 음식");

const dict = new Dict()

dict.add(kimchi);
dict.def("kimchi")
```

class의 개념의 문제인건지 타입스크립트에서 배우는데 조금 이해하기가 어려웠던거같다.

class에 대해 좀 더 자세하게 배워야겠다.
