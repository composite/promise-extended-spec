I think Promise pattern is evolution. but not ready.

# Promise/My (I think)

## Current promise pattern in action.

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

then, setInterval is still calling with increase variable `i` but never bring to then argument.

well. that's right. true. true.

but, I want to more transfer infomation to promise object. what should I do?


## Future promise pattern more can do anything I think.

### Plan A : one more promise arguments, one more case callback.

same as current promise pattern, just add one more optional arguments named as `progress`

and when calling `then`,  define one more `function` arguments for handling progress.

```js
var promise = new Promise(function(resolve, reject, progress){
  var i = 0;
  setInterval(function(){
    if(i<100){
      progress(++i);
    }else{
      resolve(i);
    }
  },1000);
});
promise.then(function(val){
  console.log("It's done!" + val + "%");
}, function(err){
  console.error("Oh, NO!" + err);
}, function(val){
  console.log("loading..." + val + "%");
});
```

This example is increase interger variable `i` at every seconds, and transfer to `progress`.

and run simple progress handler in 3rd argument of `then` function.

when `i` incresed 100, call `resolve` with increased value, and... well.. same as current promise pattern.

that's all.

 - GOOD : 
  - compatibility with current promise pattern.
 - BAD :
  - looks more dirty in `then` method.

I'll think more ways.
