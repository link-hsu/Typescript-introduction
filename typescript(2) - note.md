## Typescript
[Course Link](https://www.youtube.com/playlist?list=PL4cUxeGkcC9gUgr39Q_yD6v-bSyMwKPUI "Link here")  
[Github code](https://github.com/iamshaunjp/typescript-tutorial)
### Basics (from #10~)
- Function Signatures
  ~~~ typescript
  // let greet: Function;
  // let greet: Function = () => {
  //   console.log('hello, world');
  // }

  // example 1
  let greet: (a: string, b: string) => void;

  greet = (name: string, greeting: string) => {
    console.log(`${name} says ${greeting}`);
  }

  // example 2
  let calc: (a: number, b: number, c: string) => number;

  calc = (numOne: number, numTwo: number, action: string) => {
    if (action === 'add') {
      return numOne + numTwo;
    } else {
      return numOne - numTwo;
    }
  }

  // example 3
  let logDetails: (obj: {name: string, age: number}) => void;

  logDetails = (ninja: {name: string, age: number}) => {
    console.log(`${ninja.name} is ${ninja.age} years old`);
  }
  ~~~
- DOM
  ~~~ typescript
  const anchor = document.querySelector('a')!;
  if(anchor) {
    console.log(anchor.href);
  }
  console.log(anchor.href);

  //const form = document.querySelector('form')!;
  const form = document.querySelector('.new-item-form') as HTMLFormElement;
  console.log(form.children);

  // inputs
  const type = document.querySelector('#type') as HTMLInputElement;
  const tofrom = document.querySelector('#tofrom') as HTMLInputElement;
  const details = document.querySelector('#details') as HTMLInputElement;
  const amount = document.querySelector('#amount') as HTMLInputElement;

  form.addEventListener('submit', (e: Event) => {
    e.preventDefault();

    console.log(
      type.value, 
      tofrom.value, 
      details.value, 
      amount.valueAsNumber
    );
  });
  ~~~
- Classes
  ~~~ typescript
  // classes
  class Invoice {
    client: string;
    details: string;
    amount: number;

    constructor(c: string, d: string, a: number){
      this.client = c;
      this.details = d;
      this.amount = a;
    }

    format() {
      return `${this.client} owes £${this.amount} for ${this.details}`;
    }
  }

  const invOne = new Invoice('mario', 'work on the mario website', 250);
  const invTwo = new Invoice('luigi', 'work on the luigi website', 300);

  let invoices: Invoice[] = [];
  invoices.push(invOne)
  invoices.push(invTwo);
  // invoices.push({ name: 'shaun' });

  console.log(invoices);


  const form = document.querySelector('.new-item-form') as HTMLFormElement;
  console.log(form.children);

  // inputs
  const type = document.querySelector('#type') as HTMLInputElement;
  const tofrom = document.querySelector('#tofrom') as HTMLInputElement;
  const details = document.querySelector('#details') as HTMLInputElement;
  const amount = document.querySelector('#amount') as HTMLInputElement;

  form.addEventListener('submit', (e: Event) => {
    e.preventDefault();

    console.log(
      type.value, 
      tofrom.value, 
      details.value, 
      amount.valueAsNumber
    );
  });
  ~~~
- public, private, readonly
  ~~~ typescript
  // classes
  class Invoice {
    // readonly client: string;
    // private details: string;
    // public amount: number;

    constructor(
      readonly client: string, 
      private details: string, 
      public amount: number,
    ){}

    format() {
      return `${this.client} owes £${this.amount} for ${this.details}`;
    }
  }
  ~~~
- Modules
  ~~~ typescript
  import { Invoice } from './classes/Invoice.js';

  const invOne = new Invoice('mario', 'work on the mario website', 250);
  const invTwo = new Invoice('luigi', 'work on the luigi website', 300);

  // invOne.client = 'yoshi';
  // invOne.amount = 50;

  let invoices: Invoice[] = [];
  invoices.push(invOne)
  invoices.push(invTwo);

  invoices.forEach(inv => {
    console.log(inv.client, /*inv.details,*/ inv.amount, inv.format());
  })



  const form = document.querySelector('.new-item-form') as HTMLFormElement;
  console.log(form.children);

  // inputs
  const type = document.querySelector('#type') as HTMLInputElement;
  const tofrom = document.querySelector('#tofrom') as HTMLInputElement;
  const details = document.querySelector('#details') as HTMLInputElement;
  const amount = document.querySelector('#amount') as HTMLInputElement;

  form.addEventListener('submit', (e: Event) => {
    e.preventDefault();

    console.log(
      type.value, 
      tofrom.value, 
      details.value, 
      amount.valueAsNumber
    );
  });
  ~~~
- Interfaces
  ~~~ typescript
  import { Invoice } from './classes/Invoice.js';

  // interfaces
  export interface IsPerson {
    name: string;
    age?: number;
    speak(a: string): void;
    spend(a: number): number;
  }

  const me: IsPerson = {
    name: 'shaun',
    //age: 30,
    speak(text: string): void {
      console.log(text);
    },
    spend(amount: number): number {
      console.log('I spent ', amount);
      return amount;
    },
  };

  console.log(me);
  me.speak('hello, world');

  const greetPerson = (person: IsPerson): void => {
    console.log('hello ', person.name);
  }

  greetPerson(me);
  //greetPerson({name: 'shaun'});

  const form = document.querySelector('.new-item-form') as HTMLFormElement;
  console.log(form.children);

  // inputs
  const type = document.querySelector('#type') as HTMLInputElement;
  const tofrom = document.querySelector('#tofrom') as HTMLInputElement;
  const details = document.querySelector('#details') as HTMLInputElement;
  const amount = document.querySelector('#amount') as HTMLInputElement;

  form.addEventListener('submit', (e: Event) => {
    e.preventDefault();

    console.log(
      type.value, 
      tofrom.value, 
      details.value, 
      amount.valueAsNumber
    );
  });
  ~~~
- Interfaces with Classes
  ~~~ typescript
  import { HasFormatter } from '../interfaces/HasFormatter.js';

  export class Invoice implements HasFormatter {
    constructor(
      readonly client: string, 
      private details: string, 
      public amount: number,
    ){}

    format() {
      return `${this.client} owes £${this.amount} for ${this.details}`;
    }
  }

  import { HasFormatter } from '../interfaces/HasFormatter.js';

  export class Payment implements HasFormatter{
    constructor(
      readonly recipient: string,
      private details: string,
      public amount: number,
    ){};

    format() {
      return`${this.recipient} is owed £${this.amount} for ${this.details}`;
    }
  }

  // HasFormatter.js
  export interface HasFormatter {
    format(): string;
  }

  // app.ts
  import { HasFormatter } from './interfaces/HasFormatter.js';

  let docOne: HasFormatter;
  let docTwo: HasFormatter;

  docOne = new Invoice('yoshi', 'web work', 250);
  docTwo = new Payment('mario', 'plumbing', 200);

  let docs: HasFormatter[] = [];
  docs.push(docOne);
  docs.push(docTwo);  
  ~~~
- Generic
  ~~~ typescript
  import { Invoice } from './classes/Invoice.js';
  import { Payment } from './classes/Payment.js';
  import { ListTemplate } from './classes/ListTemplate.js';
  import { HasFormatter } from './interfaces/HasFormatter.js';

  const form = document.querySelector('.new-item-form') as HTMLFormElement;
  console.log(form.children);

  // inputs
  const type = document.querySelector('#type') as HTMLInputElement;
  const tofrom = document.querySelector('#tofrom') as HTMLInputElement;
  const details = document.querySelector('#details') as HTMLInputElement;
  const amount = document.querySelector('#amount') as HTMLInputElement;

  // list template instance
  const ul = document.querySelector('ul')!;
  const list = new ListTemplate(ul);

  form.addEventListener('submit', (e: Event) => {
    e.preventDefault();

    let doc: HasFormatter;
    if (type.value === 'invoice') {
      doc = new Invoice(tofrom.value, details.value, amount.valueAsNumber);
    } else {
      doc = new Payment(tofrom.value, details.value, amount.valueAsNumber);
    }
    
    list.render(doc, type.value, 'end');
  });

  // GENERICS

  // const addUID = (obj: object) => {
  //   let uid = Math.floor(Math.random() * 100);
  //   return {...obj, uid};
  // }

  // const addUID = <T extends object>(obj: T) => {
  //   let uid = Math.floor(Math.random() * 100);
  //   return {...obj, uid};
  // }

  const addUID = <T extends {name: string}>(obj: T) => {
    let uid = Math.floor(Math.random() * 100);
    return {...obj, uid};
  }

  let docOne = addUID({name: 'yoshi', age: 40});
  //let docTwo = addUID('shaun');

  console.log(docOne.name);

  // with interfaces
  interface Resource<T> {
    uid: number;
    resourceName: string;
    data: T;
  }

  const docThree: Resource<object> = {
    uid: 1, 
    resourceName: 'person', 
    data: { name: 'shaun' }
  };

  const docFour: Resource<string[]> = {
    uid: 1, 
    resourceName: 'shoppingList', 
    data: ['bread', 'milk']
  };

  console.log(docThree, docFour);
  ~~~
- Enums
  ~~~ typescript
  // ENUMS

  enum ResourceType { BOOK, AUTHOR, FILM, DIRECTOR };

  interface Resource<T> {
    uid: number;
    resourceType: ResourceType;
    data: T;
  }

  const docOne: Resource<object> = {
    uid: 1,
    resourceType: ResourceType.BOOK,
    data: { title: 'name of the wind' }
  }
  const docTwo: Resource<object> = {
    uid: 10,
    resourceType: ResourceType.DIRECTOR,
    data: { title: 'name of the wind' }
  }

  console.log(docOne); // index 0
  console.log(docTwo); // index 3
  ~~~