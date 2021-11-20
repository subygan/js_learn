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

