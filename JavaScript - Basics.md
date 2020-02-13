# JavaScript - Basics

JavaScript is a very flexible language. You don't have to be disciplined and you don't have to be particularly structured, to use this language. Furthermore JavaScript has a number of functions which can only be called bugs. You need to know these in order to work properly with this language. In the following chapters we'll take a closer look at the language. Basic knowledge in an object oriented language is required.

## Data types

JavaScript knows the following data types:      
- [string](#String)
- [number](#Number)
- [boolean](#Boolean)
- [null](#Null)
- [undefined](#Undefined)
- [object](#Object)

In this chapter we'll also going to take a look at these topics:
- Truthyness and Falseyness of values
- Dynamic typing

### String

You can use single or double quotes to define a string.
```javascript
> s = 'Hello World'
"Hello World"
> typeof s
"string"
```
Strings are a separate data type, but like objects have their own **methods** and **attributes**.
```javascript
> s.charAt(1) //function
"e"
> s.length //property
11
```
Like Java-Strings, JavaScript-Strings are **immutable** and work with **obejct references**. 
```javascript
> s = 'Hello World'
> t = s
> s == t
true

> s += 'test' //new string is instantiated and assigned to s
"Hello Worldtest"
> t //has not changed
"Hello World"
```

### Number

All JavaScript numbers are 64-Bit-floating-point-numbers
That's why a calculation with two integer can result in a float:
```javascript
> 1/3
0.33333333333333
```
Beside "real" numbers JavaScript also supports special values such as **NaN**, **Infinty** and **-Infinity**.
```javascript
> a = 2/undefined
NaN
> typeof a
"number" //NaN is type of number.
//It would be better if JavaScript would throw an exception at this point

> b = 8/0
Infinity
> b == Number.POSITIVE_INFINITY
true
> c = -3/0
-Infinity
```
Most Languages would throw an exception here as well. Because all numbers in JavaScript are floats, according to the IEEE-Standard infinity is used. Furthermore JavaScript natively supports the Math object which is almost the same as in Java.

### Boolean

JavaScript supports a logic data type with the literals **true** and **false**.
The following comparison operators are supported: <, >, ==, !=, <=, >=

### Null

Null is a data type with a single value: **null**.
Confusing is that null is classified as an object.
```javascript
> n = null
null
> typeof n
"object"
```
This is a JavaScript bug as well and is maintained in favor of backward compatibility. Nevertheless null is a separate data type.
It is possible to assign null to an exsisting variable with an other data type. The type will change and the reference will be deleted.
```javascript
> q = 2
2
> typeof q
"number"
> q = null
null
> typeof q
"object"
```

### Undefined

Undefined will be used if you try to access a non-existent property or if you use a variable which has not yet been declared.

### Object

All other data types in JavaScript are objects. This includes: **arrays**, **functions**, **data** and **custom objects**. For more information to objects see chapter [Objects](#Objects).

### Truthyness and Falseyness of values

It is important to know that some of the data types evaluate to true and other to false.
JavaScript handles the following as false:
- false
- 0 (null)
- "" (empty string)
- undefined
- NaN
```javascript
> 0 == false
true
```
All other types evaluate to true.
Because of that, you can write this:
```javascript
> if (a == undefined || a == NaN) {
    a = 1
}
```
like that:
```javascript
> if (!a) {
    a = 1
}
```
The same is true if you want to use a variable only if it holds a valid value:
```javascript
> if(a) {
    console.log(a)
}
```
This short form is extremely useful and is used very often in JavaScript.
Last but not least, you should understand which values are considered the same in JavaScript. It may be surprising:
```javascript
> null == undefined
true
> 5 == "5"
true
> "true" == true
false
> "1" == true
true
> "2" == true
false
```
You can see some contradictions in this example. Some typical JavaScript bugs. Null should not be equal to undefined. Even if both values are falsey, they still represent other data types. Fortunately JavaScript provides alternative equality operators:
- ===
- ==!

This operators compare variables based on their data type. The result looks much more familiar:
```javascript
> null === undefined
false
> 5 === "5"
false
> "true" === true
false
> "1" === true
false
```
Until you have a strong reason to compare values with different data types, use this alternative equality operators.
> 

### Dynamic typing



## Objects

## JSON

## Prototypes

## Functional programming

## Function arguments

## Closures

## Scope and this

## Exception handling

## Threads
