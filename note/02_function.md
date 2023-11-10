# call signature

마우스를 올렸을 때 입력과 출력에 관한 안내문

```ts
const add = (a: number, b: number): number => a + b;
```

먼저 디자인하고 코드를 구현할 수 있게 됨

```ts
type Add = (a: number, b: number) => number;

const add: Add = (a, b) => a + b;
```

# overloading

실제로 쓸 일은 많지 않지만 다른 사람이 작성한 외부 라이브러리나 패키지에서는 많이 사용함
서로 다른 여러개의 call signature를 가졌을 때 발생

```ts
type Add = {
  (a: number, b: number): number;
  (a: number, b: string): number;
};

const add: Add = (a, b) => {
  if (typeof b === "string") return a;
  return a + b;
};
```

```ts
type Config = {
  path: string;
  state: object;
};

type Push = {
  (path: string): void;
  (config: Config): void;
};

const push: Push = (config) => {
  if (typeof config === "string") {
    console.log(config);
  } else {
    console.log(config);
  }
};
```

파라미터의 개수가 다를 경우 마지막에 적은 파라미터가 옵션이 됨

```ts
type Add = {
  (a: number, b: number): number;
  (a: number, b: number, c: number): number;
};

const add: Add = (a, b, c?: number) => {
  if (c) {
    return a + b + c;
  }
  return a + b;
};
```

# polymorphism

여러 다른 형태들

generic: 타입의 placeholder 같은 개념, 타입 스크립트가 추론해서 사용할 수 있게끔 함
`<type>` 이런 형태로 앞에 적으면 됨
추가설명: https://hyunseob.github.io/2017/01/14/typescript-generic/
useState<number>()이런 식으로 사용했었음

```ts
type SuperPrint = {
  <TypePlaceHolder>(arr: TypePlaceHolder[]): void;
};

const superPrint: SuperPrint = (arr) => {
  arr.forEach((i) => console.log(i));
};

superPrint([1, 2, 3, 4]);
superPrint([true, false, true, false]);
superPrint([true, false, 3, 4]);
```

```ts
type Player<E> = {
  name: string;
  extraInfo: E;
};

const hongyeop: Player<number> = {
  name: "potato",
  extraInfo: 1,
};

type NicoExtra = {
  favFood: string;
};

type NicoPlayer = Player<NicoExtra>;

const nico: NicoPlayer = {
  name: "nicolas",
  extraInfo: {
    favFood: "kimchi",
  },
};
```
