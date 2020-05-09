### 函数默认传参
1. 在ES5中有一些函数功能需要很繁琐的操作才能完成，比如default parameter，如下代码可以模拟es5默认函数传参：
```js
function makeRequest(url, timeout, callback) {
    timeout = timeout || 2000;
  callback = callback || function(){};
  //the rest of the function
}
```
这模拟了timeout和callback这两个参数的模拟值，在这个函数中timeout为falsy值的时候会取默认值为2000，但是这引发了一个问题，假如想传的timeout值为0，也会受这个语句影响而变为2000。于是想要真正模拟默认传参还需要做一些改进：
```js
function makeRequest(url, timeout, callback) {
    timeout = (typeof timeout !== "undefined") || 2000;
  callback = (typeof callback !== "undefined")  || function(){};
  //the rest of the function
}
```
只是设定默认传参而已，就需要这么繁琐的操作，给开发带来不便，于是ES6做了一些改进，允许这样形式规定默认传参：
```js
function makeRequest(url, timeout = 2000, callback = function(){}){
    //the rest of the function
}
```
在这个函数里面url是必传的，其他两个参数如果不传都会在函数内部使用默认值2000和 `function(){}` 。

2. 另外，在ES6中，默认传参触发生效的时候并不会在arguments对象中，并且在函数内部也不能改变arguments对象（ES5非严格模式在函数内部修改参数值的话会直接改变arguments，严格模式下不会），代码如下：
```js
function mixArgs(first, second = "b") {
    console.log(arguments.length);
    console.log(first === arguments[0]);
    console.log(second === arguments[1]);
    first = "c";
    second = "d"
    console.log(first === arguments[0]);
    console.log(second === arguments[1]);
}

mixArgs("a");
//outputs:
//1
//true
//false
//false
//false
```
3. 你甚至可以在后面的参数中使用前面的参数以及调用函数：
```js
function getValue(value){
    return value + 5;
} 
function add(first, second = getValue(first)){
    return first + second;
}
console.log(add(1, 1));     // 2
console.log(add(1));        // 7
```

但是要注意的是，你不能在前面的参数的默认值赋值中使用到后面的参数：
```js
function add(first = second, second) {
    return first + second;
}
console.log(add(1, 1));         // 2
console.log(add(undefined, 1)); // throws error
```
之所以如此，是应为受暂时性死区（temporal dead zone, TDZ）规则的限制，你可以想象成是在函数调用的时候使用let依次申明了参数。
<hr>

### Rest Parameters
```js
function pick (object, ...keys){
    let result = Object.create(null);
  for (let i = 0; i < keys.length; i++){
    result[keys[i]] = object[keys[i]];
  }
  return result;
}
```
以上代码中keys是一个rest parameter,包含了所有在object之后传入的参数（arguments包括了所有的参数，含有第一个）。

**对于rest parameter的限制：** 
1. 在函数声明中rest parameter必须是最后一个参数，` function pick(object, ...keys, last) {}` 这种形式是不可取的；
```js
//SyntaxError: Rest parameter must be last formal parameter
function pick(object, ...keys, last) {
    let result = Object.create(null);
    for (let i = 0, len = keys.length; i < len; i++) {
        result[keys[i]] = object[keys[i]];
    }
    return result;
}
```

2. 不能再setter中使用rest parameter：
```js
let object = {
    //SyntaxError: Setter function argument must not be a rest parameter
    set name(...value) {
        // do something
    }
};
```