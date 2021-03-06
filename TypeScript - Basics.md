# Introduction
This is a summary of the features of TypScript and partly of next-gen JavaScript.

These topics are covered (quick access):
- [Types](#types)
- [Next-gen JS and TS](#next-gen-js-and-ts)
- [Advanced Types](#advanced-types)

Have fun!

# Types
These topics are covered in this chapter (quick access):
- [Tuples](#tuples)
- [Union Types](#union-types)
- [Literal Types](#literal-types)
- [Type Aliases](#type-aliases)
- [Function Types](#function-types)
- [Type "unknown"](#type-unknown)
- [Type "never"](#type-never)

## Tuples 
Tupels are not supported in VanillaJS. It is a fixed length and fixed typed array.
```typescript
role: [number, string];
role = [2, 'admin'];
```
the push method of arrays is an exception, meaning that the compiler does not catch this:
````typescript
role.push('author');
````

## Enums
Enum values receive a numberic value stating from 0. This behavior can be changed by assinging custom values. The second element is picking up on the assigned value of 5 and will be assigned to 6.
````typescript
enum Role { ADMIN = 5, READONLY, AUTHOR = 'also valid' }
if (Role.READONLY) {
    // do some checks
}
````

## Union Types
Role is eighter a number or a boolean:
````typescript
function combine(i1: number | string, i2: number | string) {
    // perform a runtime check
    if (typeof i1 === 'number' && ...) {
        // process some logic
    }
}
````
It is quite common to use a runtime check to be able to process different logic, based on the provided types 

## Literal Types
They are especially useful in conjunction with union types.
````typescript
function combine(
    i1: number | string, 
    i2: number | string,
    // literal types combined with union types
    // only these two values are valid
    resultConversion: 'as-number' | 'as-text') {
    let result;
    // perform a runtime check
    if (typeof i1 === 'number' && ...) {
        result = i1 + i2;
    } else {
        result = i1.toString() + i2.toString();
    }

    if (resultConversion === 'as-number') {
        return +result
    } else {
        result.toString();
    }
}
// outputs 3012 of type number
const combineStringAges = combine('30', '12', 'as-number');
````

## Type Aliases
They are also called **custom types**. Working with union types can be cumbersome and type aliases can be a good feature to simplify this.
````typescript
type Combinable = number | string;
type ConversioDescriptor = 'as-number' | 'as-text'

function combine(i1: Combinable, i2: Combinable) {
    // process logic
}
````
Type aliases are not restricted to union types, but can be used for any types:
````typescript
type User = { name: string; age: number };
const u1: User = { name: 'Max', age: 30 };
````

## Function Types
To the variable combine every function which matches this 
signature, can be assigned: 
````typescript
let combine: (a: Combinable, b: Combinable) => string;
````

### Concrete Implementation with callbacks
```typescript
function addAndHandle(a: number, b: number, cb: (n: number) 
=> void) {
    const result = a + b;
    cb(results);
}

addAndHandle(1, 3, (result) => {
    console.log(result)
});
```
>callback functions can return something, even if the
 argument on which they're passed does NOT expect a 
 returned value. The returned value will be ignored.

## Type "unknown"
Unknown is oftentimes the better choice over any, because 
it provides at least some type checking:

````typescript
userInput1: unknown;
userInput2: any;
userName: string;

userInput1 = 5;
userInput1 = 'max';
userName = userInput1; // throws a compilation error

userInput2 = 5;
userInput2 = 'max';
userName = userInput2; // doesn't throw an error
````

## Type "never"
The inferred type here would be void. If you want 
to make your intention with such a function very clear, it 
is best to do it so, using the never type. It clearly 
states, that not even undefined is returned, but instead 
the script is crashed at this point.
```typescript
function generateError(msg: string, code: number): never {
    // while(true) { } would be another use-case
    throw { message: msg, statusCode: code };
}

generateError('error occured', 500);
```

# Next-gen JS and TS
This chapter is referring to JS in the version ES6 or newer.

These topics are covered in this chapter (quick access):
- [let and const Keywords](#let-and-const-keywords)
- [Arrow Functions](#arrow-functions)
- [Default Arguments](#default-arguments)
- [Spread Operator](#spread-operator)
- [Rest Parameter](#rest-parameter)
- [Array and Object Destructuring](#array-and-object-destructuring)

## let and const Keywords
With var you do have a global and a function scope. It is 
possible to access variables which are defined globally 
from inside a function, but not in vice versa. What is not 
available with var though, is a scope within for example an 
if statement.

That is why var should be substituted with let in almost 
any case. Let and const have a different scope than var 
does. The so called **block scope**. A variable is always 
available only for the block (snipped, surrounded with 
curly braces) in which it was defined. 

## Arrow Functions
If you only have one expression, this function:
```typescript
const func = function add(a: number, b: number): number {
    return a + b;
}
```
can be shortened according to the arrow function notation:
```typescript
const func = (a: number, b: number) => a + b;
```
>This is possible, since there is always an implicit return 
statement, when using this notation.

Another neat way of using this notation is the following:
```typescript
const button = document.querySelector('button');

if (button) {
    button.addListener('click', event => console.log(event);
}
```
where it is possible to even omit the function braces.

## Default Arguments
When using default arguments, it is important, that they 
are used last in the function signature, since they are not 
skipped.
````typescript
const func = (a: number, b: number = 1) => a + b;

func(2);
````

## Spread Operator
To avoid cumbersome array operations, the spread operator 
can be used as follows:
````typescript
const hobbies = ['skiing', 'freeletics'];
const activeHobbies = ['hiking', ...hobbies];

activeHobbies.push(...hobbies);
````
The same operator can be used for objects. Keep in mind 
that here not a pointer to the old object is set, but 
instead a totally new object is created:
````typescript
const person {
    name: 'max',
    age: 30
};

const copiedPerson = { ...person };
````

## Rest Parameter
Using a unlimited and flexible amount of parameters. Here in 
combination with the reduce method provided for arrays.
````typescript
const func = (...numbers: numbers[]) => {
    return numbers.reduce((curResult, curValue) => {
        return curResult + curValue;
    });
};

func(2, 10, 6, 7.2); // outputs 25.2
````

## Array and Object Destructuring
This snipped of code does create three variables. Two with 
single string values and one new string[] with the 
remaining values from the original hobbies[].
````typescript
// does not change the original array
const [hobby1, hobby2, ...remainingHobbies] = hobbies;

// the same is possible for objects
const person {
    firstName: 'max',
    age: 30
};
/*
here you must specify the corresponding names of the 
original objects keys.
Assigning the value to a new key with a different 
identifier is possible though.
*/
const { firstName: givenName, age } = person;
console.log(givenName, age);
````
Everything above is JavaScript syntax.

# Advanced Types
These topics are covered in this chapter (quick access):
- [Intersection Types](#intersection-types)
- [Type Guards](#type-guards)
- [Discriminated Unions](#discriminated-unions)
- [Type Casting](#type-casting)
- [Index Properties](#index-properties)
- [Function Overloads](#function-overloads)
- [Optional Chaining](#optional-chaining)
- [Nullish Coalescing](#nullish-coalescing)

## Intersection Types
In case of union types, the intersection would be the types, for example of two union types. For number | string and number | boolean this would be number. 

In case of objects, the intersection is the combination of both types:
````typescript
type Employee = {
    name: string,
    startDate: Date
}

type Admin = {
    name: string,
    privileges: string[]
}

type ElevatedEmployee = Employee & Admin;

const e1 = {
    name = 'max',
    startDate = new Date(),
    privileges: ['read', 'write']
}
````
Of course, the same structure could have been set up also with the aid of interfaces. A third interface with the same type assignment including the intersection sign would then be used instead.

## Type Guards

### typeof
probably the best known type guard, which is built in VanillaJS
````typescript
function combine(a: Combinable, b: Combinable) {
    if (typeof a === 'string' ...) {
        // process logic
    }
}
`````

### in
If you use, let's say union types, it is oftentimes necessary to know which extact type is used at runtime. That is where type guards come into play.
Consider the first two type definitions from the last code example for this here:
````typescript
type UnknownEmployee = Employee | Admin;

function print(emp: UnknownEmployee) {
    // no problem to access name because it exists in both types
    console.log(emp.name);

    // if (typeof emp === 'object') does obviously would not work
    // if (emp.privileges) here the compiler would complain
    if ('privileges' in emp) {
        console.log(emp.privileges);
    }
}
````

### instanceof
Consider the following example:
````typescript
class Car {
    drive() {
        console.log('driving...');
    }
}

class Truck {
    drive() {
        console.log('driving a truck...');
    }

    loadCargo(amount: number) {
        console.log('loading: '+amount);
    }
}

type Vehicle = Car | Truck;

const v1 = new Car();
const v2 = new Truck();

function useVehicle(v: Vehicle) {
    vehicle.drive();
    if (v instanceof Truck) {
        v.loadCargo();
    }
}

````
With instanceof some extra safety is available since it is not necessary to provide a string with the correct name of a method or property which we want to access. 

## Discriminated Unions
This is a pattern, that makes working with type guards easier when using f.e. union types. It is available when working with object types.

````typescript
interface Bird {
    // a type literal type has exactly one value,
    type: 'bird';
    flyingSpeed: number;
}

interface Horse {
    // which is called discriminated union
    type: 'horse';
    runningSpeed: number;
}

type Animal: Bird | Horse;

function moveAnimal(animal: Animal) {
    let speed;
    // if (animal instanceof Horse) would not work
    // if ('runningSpeed' in animal) would also work
    switch (animal.type) {
        case 'bird':
            speed = animal.flyingSpeed;
            break;
        case 'horse':
            speed = animal.runningSpeed;
            break;
    }
    console.log('moving with speed: '+speed);
}
// we even have autocompletion when the type is set
moveAnimal({type: 'bird', flyingSpeed: 10});
````
## Type Casting
Type casting is especially usefull for example when working with the DOM.
Other than with the querySelector method, with the getElementById method, typescript is not able to infer wich exact type you will get.

````typescript
const userInput = <HTMLInputElement>document.getElementById('user-input');

//  this version exists to not clash with react syntax
const userInput = document.getElementById('user-input') as HTMLInputElement;

userInput.value = 'hi there';
````
The exclamation mark tells typescript, that this expression will never yield null. It is not needed however, when working with type casting. Another way to solve this check without the exclamation mark would be with a simple if check.
## Index Properties
With index properties, when used like in the interface below, it is possible to asign a flexible amount of properties when relying on that interface.
````typescript
interface ErrorContainer {
    [property: string]: string;
}

// also no specified property at all would be valid
const errorBag: ErrorContainer = {
    email: 'not a valid address',
    username: 'not a valid username'
}
````
## Function Overloads
With the function overloads below, it is possible narrow down what exact type will be returned when using which arguments.
````typescript
type Combinable = number | string;

function combine(i1: string, i2: string): string;
function combine(i1: number, i2: number): number;
function combine(i1: Combinable, i2: Combinable) {
    // process logic
}
````
## Optional Chaining
In bigger projects and when receiving (nested) data from a back-end, you do not always know with certainty what you will get. 

For example, assume that for some reason the job object inside the user object has not been fetched. This can be checked using the optional chaining when running on TS 3.7 or higher.
````typescript
const fetechedData = {
    id: 'u1',
    name: 'john',
    job: {
        title: 'ceo',
        description: 'my own company'
    }
    
    //the JS-way of checking if something is present:
    console.log(fetchedData.job && fetchedData.job.title);

   // the TS-way of the same check using optional chaining
   console.log(fetchedData?.job?.title);
}
````
## Nullish Coalescing

````typescript
// see this as fetched data from a back-end
const userInput = '';

/*
the logical or operator will fall back to the default 
value also when encountering falsy values like this empty 
string from userInput
*/
const storedData = userInput || 'DEFAULT';

/*
nullish coalescing falls back to the default value, only 
when the received userInput would be null or
undefinded. Therefore, here the empty string will be 
stored
*/
const storedData = userInput ?? 'DEFAULT';
````