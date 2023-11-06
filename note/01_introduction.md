# why Typescript?

## why not javascript?

타입 안정성

```js
[1, 2, 3, 4] + false;
```

```js
function devide(a, b) {
  return a / b;
}
devide("xxxxx");
```

```js
const nico = { name: "nico" };
nico.hello();
```

## how typescipt run?

타입스크립트가 코드를 먼저 확인하고
자바스크립트로 변환(compile)되기 전에 error를 사용자에게 알려줌
[Try Typescript](https://www.typescriptlang.org/play?#code/PTAEHUFMBsGMHsC2lQBd5oBYoCoE8AHSAZVgCcBLA1UABWgEM8BzM+AVwDsATAGiwoBnUENANQAd0gAjQRVSQAUCEmYKsTKGYUAbpGF4OY0BoadYKdJMoL+gzAzIoz3UNEiPOofEVKVqAHSKymAAmkYI7NCuqGqcANag8ABmIjQUXrFOKBJMggBcISGgoAC0oACCbvCwDKgU8JkY7p7ehCTkVDQS2E6gnPCxGcwmZqDSTgzxxWWVoASMFmgYkAAeRJTInN3ymj4d-jSCeNsMq-wuoPaOltigAKoASgAywhK7SbGQZIIz5VWCFzSeCrZagNYbChbHaxUDcCjJZLfSDbExIAgUdxkUBIursJzCFJtXydajBBCcQQ0MwAUVWDEQC0gADVHBQGNJ3KAALygABEAAkYNAMOB4GRonzFBTBPB3AERcwABS0+mM9ysygc9wASmCKhwzQ8ZC8iHFzmB7BoXzcZmY7AYzEg-Fg0HUiQ58D0Ii8fLpDKZgj5SWxfPADlQAHJhAA5SASPlBFQAeS+ZHegmdWkgR1QjgUrmkeFATjNOmGWH0KAQiGhwkuNok4uiIgMHGxCyYrA4PCCJSAA)

```ts
function divide(a, b) {
  return a / b;
}

divide(3);
```

입력값의 타입과 개수를 체크할 수 있다.

## 적용하기

```ts
let a = "hello";
a = "good bye";
a = 3; // error
```

처음 지정해주는 타입으로 타입 유지

```ts
let b: boolean = false;
```

```ts
let c: number[] = [1, 2, 3];
c.push("1"); // error
```

니코는 명시적 표현 보다는 타입 스크립트가 자동적으로 타입을 추론해주는 것을 권장
빈 배열일 경우에 명시적 표현 사용 권장

## basic type

```ts
let a: number[] = [1];
let b: string[] = ["hi", "hello"];
let c: boolean[] = [true];
```

## optional type

```ts
const player: {
  name: string;
  age?: number;
} = {
  name: "nico",
};
```

?를 사용할 경우 undefined가 될 수 있음을 알 수 있음

```ts
type Age = number;
type Player = {
  name: string;
  age?: Age;
};

const nico: Player = {
  name: "nico",
};

const jin: Player = {
  name: "jin",
  age: 12,
};
```

타입 재사용 가능

```ts
type Player = {
  name: string;
  age?: number;
};
function playerMaker(name: string): Player {
  return {
    name: name,
  };
}

const nico = playerMaker("nico");
nico.age;
```

아래는 화살표 함수 적용 예시

```ts
type Player = {
  name: string;
  age?: number;
};

const playerMaker = (name: string): Player => ({ name });

const nico = playerMaker("nico");
nico.age;
```

함수의 결과도 타입 지정 가능

```ts
type Player = {
  readonly name: string;
  age?: number;
};

const playerMaker = (name: string): Player => ({ name });

const nico = playerMaker("nico");
nico.name = "potaro"; // error
```

readonly 값 지정 가능

any: typescipt의 보호장치를 비활성화 시킴

### unknown

```ts
let a: unknown;

let b = a + 1; // error

if (typeof a === "number") {
  let b = a + 1;
}
```

### void

함수의 return 값이 아무 것도 없을 경우
보통 자동적으로 typescript가 인식함

### never

함수가 절대로 return하지 않을 때

```ts
function hello(name: string | number) {
  if (typeof name === "string") {
    name; // (parameter) name: string
  } else if (typeof name === "number") {
    name; // (parameter) name: number
  } else {
    name; // (parameter) name: never; 이 코드는 작동되지 말아야함
  }
}
```
