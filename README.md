# CONCEPT TYPESCRIPT

## Type Alias vs Interface

### Type (Type Alias)

-   Types basic: string, number, boolean,... .
-   Typescript has advance type and define name to type data called is `type alias`
-   **Type Alias** help reduce duplicated and allow reuse the type data in app.

```ts
type Username = string

type UserId = string | number

type User = {
    id: UserId
    name: Username
    role?: string
}
```

### Interface

-   **Interface** allow you define method or property (`object`)

```ts
interface User = {
  id: string | number
  name: string
  role?: string
}
```

-   **Interface** allow you extends `a other interface`

```ts
interface Animal {
    name: string
}

interface Bear extends Animal {
    honey: boolean
}
```

-   **Interface** can merge `interface duplicated name`

```ts
interface Bear {
    name: string
}

interface Bear {
    honey: boolean
}

const bear: Bear = {
    name: "Saigon",
    honey: true,
} // Bear has 2 property: name, honey
```

### The difference between Type and Interface

-   **Interface** can merge, **Type** `can't merge`

```ts
// INTERFACE
interface Person {
    name: string
}

interface Person {
    age: number
}

const viblo: Person = {
    name: "Viblo",
    age: 31,
}

// TYPE
type Person = {
    name: string
}

type Person = {
    age: number
}

const viblo: Person = {
    name: "Viblo",
    age: 31,
}
// error: Duplicate identifier 'Person'
```

-   **Type** can use computed properties, **Interface** no

```ts
// TYPE
type keys = "firstname" | "lastname"

type Person = {
    [key in keys]: string
}

const person: Person = {
    firstname: "Viblo",
    lastname: "blog",
}

// INTERFACE
type keys = "firstname" | "lastname"

interface Person {
    [key in keys]: string
}
// error: A computed property name in an interface must refer to an expression whose type is a literal type or a 'unique symbol' type
```

-   **Extend** and **Implements**: Interface can use **extends**, type no

```ts
interface Animal {
    name: string
}

interface Bear extends Animal {
    honey: boolean
}
```

-   **Intersection**: allow you combine a lot of type **to** a type aggregate, by use `&`

```ts
// TYPE
type Name = {
  name: string
}

type Age = {
  age: number
}

type Person = Name & Age

// INTERFACE
interface Name {
  name: “string”
}

interface Age {
  age: number
}

type Person = Name & Age
```

## Union types

-   A variables can assigned **more than** types.

```ts
let age: number | string
age = 26
age = "26"
```

## Literal types

-   We can refers to specific **string** or **number** in type positions.

```ts
let direction: "UP" | "DOWN"
direction = "UP"
```

## Tuples

-   **Tuples** is a special type of array about data type at each index. They're **stricter** than regular arrays.

```ts
let options: [string, number]
options = ["UP", 10]

// AND WE CAN PUSH ARRAY BUT CORRECT INCLUDE TYPE options DEFINE
options.push(20)
options.push("DOWN")
options.push([]) // `error` because array is not in TYPE options
options.push({}) // `error` because object is not in TYPE options
options.push(true) // `error` because boolean is not in TYPE options
```

## Enums

## Narrowing

-   Occurs when a variable moves from a less precise type to a more precise type. (`Tức là, nó xảy ra khi 1 biến biến từ 1 type ít chính xác hơn thành 1 type chính xác hơn`)

```ts
let age = getUserAge()
age // string | number
if (typeof age === "string") {
    age // string
}
```

## Generic

-   **Generic** allow for type safety in component where the arguments and return types are unknown ahead of time. (`Tức là, cho phép các type an toàn trong component mà argument và kiểu trả về không xác định được`)
-   **Generic** like `argument a type`

```ts
interface HasLength {
    length: number
}

// logLength accepts all types with a length property
const logLength = <T extends HasLength>(a: T) => {
    console.log(a.length)
}

// TS "captures" the type implicitly
logLength("Hello") // 5

// Can also explicitly pass the type to T
logLength<number[]>([1, 2, 3]) // 3
```

-   **Generic** have type `T`
