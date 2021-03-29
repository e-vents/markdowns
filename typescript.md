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
To the variable combine every function which matches this signature, can be assigned: 
````typescript
let combine: (a: Combinable, b: Combinable) => string;
````

### Concrete Implementation with callbacks
```typescript
function addAndHandle(a: number, b: number, cb: (n: number) => void) {
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
Unknown is mostentimes the better choice over any, because it provides at least some type checking:

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
The infered type here would actually be void. If you want to make your intention with such a function very clear, it is best to do it so, using the never type. It clearly states, that not even undefined is returned, but instead the script is crashed at this point.
```typescript
function generateError(msg: string, code: number): never {
    throw { message: msg, statusCode: code };
}

generateError('error occured', 500);
```

