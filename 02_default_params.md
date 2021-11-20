## Default Prameters

## TL;DR

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
