## Typescript
[Course Link](https://www.youtube.com/playlist?list=PL4cUxeGkcC9gNhFQgS4edYLqP7LkZcFMN "Link here")  
[Github code](https://github.com/iamshaunjp/typescript-masterclass)
### Basics
- Built **on top of javascript**
- javscript is loosely typed; typescript is **strongly typed**
- **Better autocompletion when using Vscode** -> apply autocompletion hint we can use
- Help **fix errors**
- **Custom types** for customize setting
### Syntax
- 1. Install
     ```npm install -g typescript```  
  2. create file  
     *index.ts*
  3. compile ts file
     ```tsc index.ts```
- tsconfig file  
  ```tsc --init```
  ~~~ javascript
  {
    "compilerOptions": {
      ...
      "rootDir": "./src",
      "outDir": "./dist",
    }
  }
  ~~~
  ```tsc --watch```
  ```node dist/index.js --watch```
- primitive types
  ~~~ typescript
  let age: number = 30;
  let firstName: string = 'Mario';
  let isFictional: boolean;

  // null & undefined
  let something: null;
  let anotherThing: nudefined;
  ~~~
- arrays
  ~~~ typescript
  let names: string[] = ['mario', 'luigi', 'peach']
  let ages: number[] = [25, 28, 24]
  let myArray: (string | number)[] = [1, "two", 3]

  // names.push(true)
  names.push('bowser')

  // ages.push('35')
  ages.push(30)
  ~~~
- type inference with arrays
  ~~~ typescript
  let fruits = ['apples', 'pears', 'bananas', 'mangos']

  // fruits.push(20)
  fruits.push('peaches')

  const f = fruits[3] // infers the type based on fruits type: string

  let things = [1, true, 'hello']

  const t = things[0] // can be any of the types initially added: string | number | boolean
  ~~~
- object literals
  ~~~ typescript
  let user: { firstName: string; age: number; id: number } = {
    firstName: 'mario',
    age: 30,
    id: 1,
    // isFictional: true
  }

  // user.name = 25
  // user.email = 'peach@netninja.dev'
  user.firstName = 'peach'
  user.id = 2

  // destructuring from objects
  const { age, id }: { age: number; id: number } = user
  ~~~
- type inference with object literals
  ~~~ typescript
  let person = {
    name: 'luigi',
    score: 35,
  }

  // person.name = true
  // person.id = 3
  person.name = 'bowser'

  const score = person.score // infers number type
  ~~~
- functions
  ~~~ typescript
  function addTwoNumbers(a: number, b: number): number {
    return a + b
  }

  const subtractTwoNumbers = (a: number, b: number): number => {
    return a - b
  }

  // addTwoNumbers('2', 5)
  addTwoNumbers(3, 9)
  subtractTwoNumbers(10, 7)

  function addAllNumbers(items: number[]): void {
    const total = items.reduce((a, c) => a + c, 0)
    console.log(total)
  }

  addAllNumbers([5, 7, 9, 11, 3, 2, 1])
  ~~~
- return type inference
  ~~~ typescript
  function formatGreeting(name: string, greeting: string) {
    return `${greeting}, ${name}`
  }

  // we get inference on return types, but not on argument types
  // type inference on return values does not enforce a return type
  ~~~
- any type
  ~~~ typescript
  let age: any
  let title

  age = 30
  age = false

  title = 25
  title = {
    hello: 'world',
  }
  ~~~
- any type in arrays
  ~~~ typescript
  let things: any[] = ['hello', true, 30, null]

  things.push({ id: 123 })
  ~~~
- functions & any
  ~~~ typescript
  function addTogether(value: any): any {
    return value + value
  }

  const resultOne = addTogether('hello')
  const resultTwo = addTogether(3)

  // useful when migrating from js to ts
  // because using any won't cause errors initially
  ~~~
- tuples
  ~~~ typescript
  let person: [string, number, boolean] = ['mario', 30, true]

  // person[0] = false
  person[0] = 'luigi'

  // tuples examples
  let hsla: [number, string, string, number]
  hsla = [200, '100%', '50%', 1]

  let xy: [number, number]
  xy = [94.7, 20.1]

  function useCoords(): [number, number] {
    // get coords of something

    const lat = 100
    const long = 50

    return [lat, long]
  }

  const [lat, long] = useCoords()
  ~~~
- named tuples
  ~~~ typescript
  let user: [name: string, age: number]

  user = ['peach', 25]
  console.log(user[0])
  ~~~
- interfaces
  ~~~ typescript
  interface Author {
    name: string
    avatar: string
  }

  const authorOne: Author = { name: 'mario', avatar: '/img/mario.png' }

  interface Post {
    title: string
    body: string
    tags: string[]
    created_at: Date
    author: Author
  }

  const newPost = {
    title: 'my first post',
    body: 'something interesting',
    tags: ['gaming', 'tech'],
    created_at: new Date(),
    author: authorOne,
  }
  ~~~
- as function argument types
  ~~~ typescript
  function createPost(post: Post): void {
    console.log(`created post ${post.title} by ${post.author.name}`)
  }

  // createPost({ title: 'a new post title' })
  createPost(newPost)
  ~~~
- with arrays
  ~~~ typescript
  let posts: Post[] = []

  // posts.push({ title: 'some title' })
  posts.push(newPost)
  ~~~
- type aliases
  ~~~ typescript
  // example 1 - tuple

  type Rgb = [number, number, number]

  function getRandomColor(): Rgb {
    const r = Math.floor(Math.random() * 255)
    const g = Math.floor(Math.random() * 255)
    const b = Math.floor(Math.random() * 255)

    return [r, g, b]
  }

  const colorOne = getRandomColor()
  const colorTwo = getRandomColor()
  console.log(colorOne, colorTwo)

  // example 2 - object literal

  type User = {
    name: string
    score: number
  }

  const userOne: User = { name: 'mario', score: 75 }

  function formatUser(user: User): void {
    console.log(`${user.name} has a score of ${user.score}.`)
  }

  formatUser(userOne)
  formatUser({ name: 'yoshi', score: 100 })
  ~~~
- union types
  ~~~ typescript
  let someId: number | string

  someId = 1
  someId = '2'

  let email: string | null = null

  email = 'mario@netninja.dev'
  email = null

  type Id = number | string
  let anotherId: Id

  // anotherId = undefined
  anotherId = '1'
  anotherId = 2
  ~~~
- union type pitfall
  ~~~ typescript
  function swapIdType(id: Id): Id {
    // can only use props and methods common to
    // both number and string types
    // parseInt(id) --> not allowed

    return id
  }
  ~~~
- type guards
  ~~~ typescript
  // example 1

  type Id = number | string

  function swapIdType(id: Id): Id {
    if (typeof id === 'string') {
      // can use string methods and properties
      return parseInt(id)
    } else {
      // can use number methods and properties
      return id.toString()
    }
  }

  const idOne = swapIdType(1)
  const idTwo = swapIdType('2')

  console.log(idOne, idTwo)
  ~~~
- tagged union types
  ~~~ typescript
  interface User {
    type: 'user'
    username: string
    email: string
    id: Id
  }
  interface Person {
    type: 'person'
    firstname: string
    age: number
    id: Id
  }

  function logDetails(value: User | Person): void {
    if (value.type === 'user') {
      console.log(value.email, value.username)
    }
    if (value.type === 'person') {
      console.log(value.firstname, value.age)
    }
  }
  ~~~