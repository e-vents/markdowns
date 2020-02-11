# JavaScript - Basics
JavaScript is a very flexible language. You don't have to be disciplined and you don't have to be particularly structured, to use this language. Furthermore JavaScript has a number of functions which can only be called bugs. You need to know these in order to work properly with this language. In the following chapters we'll take a closer look at the language. Basic knowledge in an object oriented language is required.
## Data types
JavaScript knows the following data types
- string
- number
- boolean
- null
- undefined
- object
### Strings
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
Like Java-Strings JavaScript-Strings are immutable and work with obejct references. 
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
### Numbers

### Boolean

### Undefined

### Object

### Truthyness and Falseyness of values

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
