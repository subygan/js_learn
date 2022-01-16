---
layout: base
type: page
emoji: 7️⃣
title: Syntax
description: 
date: yyyy-mm-dd 22:15:00
---

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


