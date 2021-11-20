### Understanding const

The `const` keyword creates a read-only reference to a value.

```js
const CONSTANT_NAME = value;
```

By convention, the constant identifiers are in uppercase. it can be lower case as well though. the variable made from `let` and `var` are mutable. But, const can't be changed

```js
const RATE = 0.1;
RATE = 0.2; //TypeError
```

Declaring a const without initialising with a value also creates a SyntaxError

```js
const RED; //SyntaxError
```

### JavaScript const and Objects

The `const` keyword ensures that the variable it creates is read-only. However, it doesn't mean that the actual to which the `const` variable reference is immutable.

```js
const person = { age: 20 };
person.age = 30; // This works!!
console.log(person.age); // 30  :
```

#### Object.freeze()

If it is required for the object to be immutable, you have to freeze it by using the `Object.Freeze()` method:

```js
const person = Object.freeze({age:20});
person.age = 30; //TypeError
```

Objects one level deeper are not frozen

```js
const company = Object.freeze({
    name: 'new name',
    address: {
        street: 'North 1st street',
        city: 'san jose'
    }
})
```

But the `company.address` object is not immutable, you can add a new property to the `company.address` object as follows:

```js
company.address.country = 'USA'; //OK
```

#### JavaScript const and Arrays

Consider the following example:

```js
const colors = ['red'];
colors.push('green');
console.log(colors); // ["red", "green"]

colors.pop(); // This works
colors.pop(); // this works as well
console.log(colors); // []


colors = []; // TypeError : This doesn't work
```

### const in a for loop

There is a construct in ES6 called `for...of` that allows to create a loop iterating over iterable objects such as arrays, maps, and sets.

```js
let scores = [75, 80, 95];

for (let score of scores) { //This works
    //   ^^^^^ This creates a variable from an iterator  
    console.log(score);
}
```

```js
for (const i = 0; i < scores.length; i++) { //TypeError
    console.log(scores[i]);
}
```