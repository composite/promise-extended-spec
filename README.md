I think Promise pattern is evolution. but not ready.

# Promise/My (I think)
## Promise pattern for more cases.

### Promise/A or A+ Standard

```js
var promise = new Promise(function(resolve, reject){
  var i = 0;
  setInterval(function(){
    resolve(++i); // when fired, this promise will flag with DONE.
  });
});
promise.then(function(i){
  console.log(i);
}).then(function(i){
  console.log(i);
});
```

Console output as,

`1`
`1`

Yes, when call resolve function, that promise will think "My promise has done!".
then, setInterval is still calling, but never increase variable `i`.

