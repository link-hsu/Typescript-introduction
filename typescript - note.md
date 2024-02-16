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
- arrays
  ~~~ typescript
  let names: string[] = ['mario', 'luigi', 'peach']
  let ages: number[] = [25, 28, 24]

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

  const f = fruits[3] // infers the type based on fruits type

  let things = [1, true, 'hello']

  const t = things[0] // can be any of the types initially added
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