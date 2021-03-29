
# Types

## Tuples 
are not supported in VanillaJS. It is a fixed length and fixed typed array.
```typescript
role: [number, string];
role = [2, 'admin'];
```
the push method of arrays is an exception, meaning that the compiler does not catch this:
````typescript
role.push('author');
````

## Enum
Enum values receive a numberic value stating from 0. This behavior can be changed by assinging custom values. The second element is picking up on the assigned value of 5 and will be assigned to 6.
````typescript
enum Role { ADMIN = 5, READONLY, AUTHOR = 'also valid' }
if (Role.READONLY) {
    // do some checks
}
````

## Union Type
Role is eighter a number or a boolean:
````typescript
function combine(i1: number | boolean, i2: number | boolean) {
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
## Type Aliases / Custom Types
Working with union types can be cumbersome and type aliases can be a good feature to simplify this.
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
hint: callback functions can return something, even if the
 argument on which they're passed does NOT expect a 
 returned value. The returned value will be ignored.

## Type "unknown"
Unknown is mostentimes the better choice over any, because 
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
The infered type here would actually be void. If you want 
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

# Next-gen JavaScript and TypeScript
This chapter is refering to JS in the version ES6 or newer.
## let and const keywords
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
This is possible, since there is always an implicit return 
statement, when using this notation.

Another neat way of using this notation is the following:
```typescript
const button = document.querySelector('button');

if (button) {
    button.addListener('click', event => console.log(event);
}
```
where it is possible to even emit the function braces.

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
that here not a pointer to the old obejct is set, but 
instead a totally new object is created:
````typescript
const person {
    name: 'max',
    age: 30
};

const copiedPerson = { ...person };
````

## Rest Parameter
Using a unlimited and fleible amount of parameters. Here in 
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

// here you have to specify the corresponding names of the 
original obejcts keys.
// assinging the value to a new key with a different 
identifier is possible though.
const { firstName: givenName, age } = person;
console.log(givenName, age);
````
Everything above is JavaScript syntax.

# Advanced Types
