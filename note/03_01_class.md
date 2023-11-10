# Classes

접근 가능위치
private: 선언 클래스 내 o, 상속받은 클래스 내 x, 인스턴스 x
protected: 선언 클래스 내 o, 상속받은 클래스 내 o, 인스턴스 x
public: 선언 클래스 내 o, 상속받은 클래스 내 o, 인스턴스 o

```ts
class Player {
  constructor(
    private firstName: string,
    private lastName: string,
    public nickname: string
  ) {}
}

const nico = new Player("nico", "las", "니꼬");

nico.nickname;
```

추상 클래스: 상속 가능한데 직접 생성은 불가능

```ts
abstract class User {
  constructor(
    private firstName: string,
    private lastName: string,
    public nickname: string
  ) {}
}

class Player extends User {}
const nico = new Player("nico", "las", "니꼬");

nico.nickname;
```

추상 메소드: 추상 클래스를 상속 받는 모든 것들이 구현해야하는 메소드를 의미, 상속 받는 클래스에서 구현해줘야 함
private으로 선언할 경우, 상속 받는 클래스에서 this로 값을 받을 수 없음
protected를 사용하여, 상속 받는 클래스에서 this로 값을 받을 수 있게 할 수 있음

```ts
abstract class User {
  constructor(
    private firstName: string,
    private lastName: string,
    protected nickname: string
  ) {}
  abstract getNickName(): void;
}

class Player extends User {
  getNickName() {
    console.log(this.nickname);
  }
}
const nico = new Player("nico", "las", "니꼬");

nico.getNickName();
```

객체의 props의 이름에도 타입을 지정해 줄 수 있다

```ts
type Words = {
  [key: string]: string;
};

let dict: Words = {
  potato: "food",
};
```

```ts
type Words = {
  [key: number]: string;
};

let dict: Words = {
  1: "food",
};
```

The constructor method is a special method of a class for creating and initializing an object instance of that class.
class도 타입처럼 사용이 가능

```ts
type Words = {
  [key: string]: string;
};

class Dict {
  private words: Words;
  constructor() {
    this.words = {};
  }
  add(word: Word) {
    if (this.words[word.term] === undefined) {
      this.words[word.term] = word.def;
    }
  }
  def(term: string) {
    return this.words[term];
  }
}

class Word {
  constructor(public term: string, public def: string) {}
}

const kimchi = new Word("kimchi", "Korean food");

const dict = new Dict();

dict.add(kimchi);
dict.def("kimchi");
```

내가 조금 수정한 코드
public 뒤에 readonly를 붙이면 읽기는 가능하지만 수정은 불가능해짐

```ts
type Words = {
  [key: string]: string;
};

class Dict {
  private words: Words;
  constructor() {
    this.words = {};
  }
  add(word: Word) {
    if (this.words[word.term] === undefined) {
      this.words[word.term] = word.def;
    } else {
      console.log(`${word.term} already exists`);
    }
  }
  update(word: Word) {
    this.words[word.term] = word.def;
  }
  remove(term: string) {
    if (this.words[term] !== undefined) {
      delete this.words[term];
      console.log(`delete ${term} successfully`);
    } else {
      console.log(`${term} does not exist`);
    }
  }
  def(term: string) {
    if (this.words[term] === undefined) {
      return console.log(`${term} does not exist`);
    } else {
      return this.words[term];
    }
  }
}

class Word {
  constructor(public readonly term: string, public readonly def: string) {}
}

const kimchi = new Word("kimchi", "Korean food");

const dict = new Dict();

dict.add(kimchi);
dict.def("kimchi");
```
