## template strings - tagged
description: the 1st parameter receives only the pure strings of the template string  
First, template string can also be used as tagged function:  
```js
alert`hi` = alert('hi')

let tagfunc = function(s){
   return s;
}
tagfunc`hi`;
```  
With the result above, I found that the parameter of tagged function is an array which is `["hi", raw: Array(1)]`. Therefore, if I want to return a pure string, I can use:  
```js
tagfunc`hi`[0];
tagfunc`hi`.raw[0];
```  

description:  
the 2nd parameter contains the first expression's value  
the 3rd parameter contains the second expression's value  
using ES6 rest syntax, all values can be accessed via one variable  
```js
var one = 1, two = 2;
function test(strings, first, second){
    console.log(strings, first, second);
}
test`the first param is ${one} and the second param is ${two}!!`
```  
strings: `["The first param is ", " and the second param is ", "", raw: Array(3)]`  
first: `1`  
second: `2`  
After all, using `(strings, ...all)`, `all` can put all the parameter value into an array at the same time!  

## template strings - String.raw
description: raw can access the backslash of a line-break  
I found that `String.raw()` and `str.raw` return different type of result.  
`String.raw()` return string.  
`str.raw` return array.  
Therefore, in order to access the blackslash from line-break  
```js
str = `\n`
str.raw.toString()[0]
```  
The first char would be blackslash.  

description: works on unicodes too  
What is different is that `'\u{1F600}'` unicode character doesn't need any backtip to wrap it then can interpret it.  

## Object - is
description: coercion, as in `==` and `===`, does NOT apply
```js
Object.is(1, 1)  // true
Object.is(1, '1')   // false
let coerced = +0 === -0;  // true
Object.is(+0, -0)   // false
NaN == NaN   // false
Object.is(NaN, NaN)  // true
Object.is(NaN, 0/0)   // true
Object.is({}, {})   // false
```  
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/is
According to the reference, `Object.is` won't make coercion on the both side value just as `==` and `===`!
