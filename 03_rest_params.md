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
