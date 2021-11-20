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