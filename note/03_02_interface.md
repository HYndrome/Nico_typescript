`Type`은 오브젝트의 모양(alias)을 묘사하는데 사용할 수 있음
`Type`은 또한 특정 값을 가지도록 사용할 수 있음

```ts
type Team = "red" | "blue" | "yellow";

type Player = {
  nickname: string;
  team: Team;
};
```

# interface

`interface`는 오직 `오브젝트`의 모양을 묘사하는 하나의 목적에만 사용
`type`은 다양하게 사용

```ts
type Team = "red" | "blue" | "yellow";

interface Player {
  nickname: string;
  team: Team;
}
// 아래는 거의 같은 기능을 함
type Player = {
  nickname: string;
  team: Team;
};
```

interface는 class처럼 상속 받을 수 있다

```ts
interface User {
  name: string;
}

interface Player extends User {}

const nico: Player = {
  name: "nico",
};
```

타입으로 상속 받을 경우

```ts
type User = {
  name: string;
};

type Player = User & {};

const nico: Player = {
  name: "nico",
};
```

interface는 축적(cumulate)이 가능 / type은 불가능

```ts
interface User {
  name: string;
}

interface User {
  lastName: string;
}

interface User {
  health: number;
}

const nico: User = {
  name: "nico",
  lastName: "las",
  health: 5,
};
```
