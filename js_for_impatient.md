---
emoji: 📕
title: Learning JavaScript
description: Learning notes form axel Rauschmayer's javascript for impatient programmers
date: 2022-11-06
layout: base
---

These are my notes from following the excellent book, [javascript for impatient programmers](https://exploringjs.com/impatient-js/index.html) by axel Rauschmayer

### Understanding let and var

The `let` keyword creates a new variable locally. it is **not attached to the global object**

```jsx
let x = 10; //creating a variable
if x == 10 {
	let x = 20;
	console.log(x); //prints 20
}

console.log(x); //prints 10
//         ^^^ This x comes from above
```

The `var` keyword creates a **new variable globally**.

```jsx
var a = 10;
let b = 10;
console.log(window.a); //10        :because the variable is available globally
console.log(window.b); //undefined :because the variable is not available globally
```

One bad thing that happens due to this is.

```jsx
for (var i = 0; i<5; i++){
	setTimeout(function(){
		console.log(i);
	}, 1000);

/*
prints 
5
5
5
5
5

because i was declared as a 'var'and hence 
is global so when it is called from the queue.
i has been updated to 5 and only that is accessible
*/

for (let j=1; j<5; j++){
	setTimeout(function(){
		console.log(i);
	}, 1000);
/*
prints
1
2
3
4
5

because i was declared locally when this is pushed to the
stack, it has a local value present with it
*/
```

### Redeclaration

var lets you redeclare variables

redeclaring a variable using the `let` keyword result in an error:

```jsx
let counter = 0;
let counter;
console.log(counter);
```

This results in an error like,

```bash
Uncaught SyntaxError: Identifier 'counter' has already been declared
```

### Temporal Death Zone (TDZ)

A variable declared by the `let` keyword has a so-called temporal dead zone (TDZ). The TDZ is the time from the start of the block until the variable declaration is processed.

example that temporal dead zone is time-based, not location-based.

```jsx
{ //entering new scope, TDZ starts here
	let log = function () {
		console.log(message);
	};

	//This is the TDZ and accessing log
	//would cause a ReferenceError

	let message = 'Hello'; //TDZ ends
  log(); //called outside TDZ hence will return some value.
}
```

Firstly, the curly brace starts a new block scope, therefore, the TDZ. start.

Second the `log()` function expression acesses the `message` variable. However, the `log()` function has not been executed yet.

Third, declare the `message` variable and initialize its value to 10. The time from the start of the block scope to the time that the message variable is accessed is called a *temporal death zone*. When the JavaScript engine processes the declaration, the TDZ ends.

The final call to `log()` function accesses the `message` variable outside of the TDZ.

It should be noted that if you access a variable declared by the `let` keyword in the TDZ, you'll get a `ReferenceError` as illustrated in the following example.

```jsx
{
	console.log(typeOf myVar); //undefined
	console.log(typeOf message); //ReferenceError
	
	let message;//TDZ ends here
	var myVar;
}
```

The temporal death zone is there to **prevent you from accidently referencing a variable before its declaration.**

## Default params

```js
function say(message='Hi') {
    console.log(message)
}

say(); // 'Hi'
say('Hello'); //'Hello'
```

### Arguments vs Parameters

Parameters - what is specified in the function declaration

Arguments - what is __passed__ to the function

```js
function add(x,y) {
    //       ^ ^ Parameters
    return x+y;
}

add(100, 200);
//  ^^^  ^^^ Arguments
```

### JS History

- Founded by Brendan Eich for netscape navigator.
- *JavaScript*  => language and its implementations
- *ECMAScript* => language standard and language versions

## ECMA Technical Committee39 (TC39)
Meetings occur every 2 months, the meeting notes can be found in [this github repo](https://github.com/tc39/notes)

New proposals are tracked through [this github repository for proposals](https://github.com/tc39/proposals)

## JavaScript rest parameters

The rest parameter, shown as `(...)`. A __rest parameter allows you to represent an indefinite number of arguments as an array__.

```js
function fn(a,b,...args) {
    //          ^^^^^^^ rest parameter available as an array of elements  
    for (const a of args){
        //do something with a
    }
}
```

rest parameters are available as an array

### wrong way to declare a rest parameter

```js
function fn(a,...rest,b) {
    //error
}
```

## Using Spread operators

Spread operators are used to combine arrays, maps or set.

```js
const odd = [1,3,5];
const combined = [2,4,6, ...odd]; //valid spread
const combined1 = [2, ...odd, 4, 6]; //valid as well

console.log(combined); // [2,4,6,1,3,5]
console.log(combined1); // [2,1,3,5,4,6]
```

the syntax is similar to [rest params](03_rest_params.md)

## Using spread params:

```js
var variables = ['a', 'b'];
var newvars = ['c', 'd'];

variables.push(...newvars);
console.log(variables); // ['a','b','c','d']
```
concatenating arrays
```js
let num = [1,2];
let num2 = [3,4];
let allnums = [...num,...num2]
```

copying an array
```js
let scores = [80, 70, 90]
let newscores = [...scores]
```

spread operator and strings

```js
let chars = ['A', ...'BC', 'D'];
console.log(chars); //["A", "B", "C", "D"]
```

### object literal

The goal of this  moodely is to make _object literals_ more succinct and powerful by extending the syntax in some ways.

### Object property initializer shorthand

```js
 function createMachine(name, status) {
    
    //old way of initializing object
    return {
        name: name,
        status: status
    }
}

function createMachineNew(name, status){
    //new way of initializing object
    return {
        name,
        status
    }
}
```

other ways of initialising

```js
name = 'computer';
status = 'on';

//This works as well
let machine = {
    name,
    status
};
```

### Computed property name

Prior to ES6, you could use the square brackets (`[]`) to enable the computed property names for the properties on objects.


```js
let name = 'machine name';
let machine = {
    [name]: 'server', // the key here is 'machine name' and can be accessed as machine['machine name']
    ["machine hours"]: 10000
}
```

### Concise method syntax

while defining methods, name and full function definition was required. now it's not

```js
let server = {
    name: 'Server',
    restart: function (){ //old way of defining
        console.log("restart() is running")
    },
    restartNew() { //new way of defining
        console.log("restartNew() is running")
    },
    'restart NEW'() { //this method can e run by server['restart NEW']()
        console.log("this is insane!!!!")
    }
}
```

## Basic constructs

### Comments:

```js
// Single-line comment

/*
comment wit multiple lines
*/

```

### Primitive values:

Booleans:

    true
    
    false

Numbers:

    1.141

    -123

The number type is __used for both floating point numbers and integers.__
Can only represent integers within a range of 53 bits + sign

Bigints:

    17n
    
    -149n

Bigints can grow to arbitrarily large number

Strings:

    'abc'
    "abc"
    `string with interpolated values: ${256} and ${true}`

JavaScript has no extra type for characters. It uses strings to represent characters

### Assertions

an *assertion* describes what the result of a computation is expected to look like and throws excaption when it fails

```js

assert.equal(7+1,8);
assert.equal(7+1,7);

```

### Logging to the console

Console logging can be used with both nodejs and browser.
The console API has a lot of customisations possible that can be found [here](https://developer.mozilla.org/en-US/docs/Web/API/console)

### Operators

```js
//Operators for booleans
assert.equal(true && false, false) //And
assert.equal(true || false, true) //Or

//Operators for numbers
assert.equal(3 + 4, 7);
assert.equal(5 - 1, 4);
assert.equal(3 * 4, 12);
asssert.equal(10 / 4, 2.5);

//Operators for bigints
assert.equal(3n + 4n, 7n);
assert.equal(5n - 1n, 4n);
assert.equal(3n * 4n, 12n);
asssert.equal(10n / 4n, 2.5n);

//Operators for strings
assert.equal('a'+'b', 'ab');
assert.equal('I see' + 3 + 'monkeys', 'I see 3 monkeys');

//Comparison operators
assert.equal( 3 < 4, true);
assert.equal( 3 <= 4, true);
assert.equal( 'abc' === 'abc', true); //AKA strict equal
assert.equal( 'abc' !== 'def', true);
```

### Declaring variables

`const` =>
- *immutable variable bindings
- Everything must be initialised immediately, different values cannot be assigned later.

```js
const x = 8;

x = 9; // <== would create issue
```

`let` =>

let create *mutable variable bindings

```js
//Declaring y (mutable binding):
let y = 35;
```

### Ordinary function declaration

```js
//add1() has the parameters a and b
function add1(a,b) {
    return a + b
}
//calling function add1()
console.log(ad1(5,2))
```
### Arrow function expressions

These are usually used as arguments of function calls ad method calls

```js
const add2 = (a,b) =>{ return a+b }; //Valid arrow function
const add3 = (a,b) => a+b; //Also valid

console.log(add2(1,2)); //works similar to a normal function
```

### Plain objects

```js
const obj = {
    first: 'Jane',
    last: 'Doe',
    getfullname() {
        return this.first + ' ' + this.last;
    }
}

console.log(obj.first) //Jane
obj.first = 'Janey';
console.log(obj.getfullname()) //Janey Doe
```
### Arrays

```js
//Array using an Array literal
const arr = ['a','b','c']

arr[0] = '4' //Array can be edited even if it is a const

arr.push('d') //appending an element to an array
```

### Modules
Every module is a file.

Each module is a single file. For example,

    file-tools.mjs
    main.mjs

The module in `file-tools.mjs` exports its function `isTextFilePath()`:

```js
export function isTextFilePath(filePath) {
    return filePath.endsWith('.txt');
}
```

The module in `main.mjs` imports the whole module *path* and the function *isTextFilePath():

```js
//Import whole module as namespace object 'path'
import * as path from 'path';
//Import a single export of module file-tools.mjs
import {isTextFilePath} from './file-tools.mjs';
```

### classes

```js
class Person {
    constructor(name){
    this.name = name;
    }
    describe() {
        return `Person named ${this.name}`;
    }
    static logNames(persons) {
        for (const person of persons) {
            console.log(person.name)
        }
    }
}

class Officer extends Person {
    constructor(name, title) {
        super(name);
        this.title = title;
    }
    describe() {
        return super.describe() + `(${this.title})`;
    }
}
const olivier = new Officer('Olivier','CTO')
console.log(olivier) //Person named Jane (CTO)
```

### Exception handling

```js


