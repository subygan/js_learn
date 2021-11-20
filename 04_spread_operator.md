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

