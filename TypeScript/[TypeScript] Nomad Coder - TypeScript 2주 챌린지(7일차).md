다형성, 제네릭, 클래스, 인터페이스를 모두 합쳐보자.

다형성은 다른 모양의 코드를 가질 수 있게 해주는 것,

다형성을 이룰 수 있는 방법은 제네릭을 사용해야한다!

```
interface SStorage<T> {
  [key:string]: T  // key가 제한되지 않은 오브텍트를 정의하게 해줌
}

class localStorage<T> {
  private storage: SStorage<T> = {}
  set(key:string, value:T){
    this.storage[key] = value;
  }
  remove(key:string){
    delete this.storage[key]
  }
  get(key:string):T {
    return this.storage[key]
  }
  clear(){
    this.storage = {}
  }
}

const stringsStorage = new LocalStorage<string>()

stringsStorage.get("ket")
stringsStorage.set("hello", "how are you")

const booleansStorage = new LocalStorage<boolean>()

booleansStorage.get("xxx")
```
