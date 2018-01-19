Values
=======
## Arrays
 containers for any type of Value

```javascript
var a = [1, "2", [3]];

a.length; // 3
a[0] === 1; //true
a[2][0] === 3 // true
```

```javascript
var a =[];

a.length; // 0
a[0] = 1;
a[1] = "2";
a[2] = [3];

a.length; // 3
```

```javascript
var  a = []

a[0] = 1;
// no 'a[1]' slot set here
a[2] = [3];
a[1]; // undefined

a.length; //3
```
arrays also are objects

```javascript
var a = [];

a[0] = 1;
a["foobar"] = 2;

a.length;    // 1
a["foobar"]; // 2
a.foobar     // 2
```
a `string` value intented as a key can be coerced to a standard base 10 `number`.

```javascript
var a = [];
a["13"] = 42;
a.length; //14
```

#### Array-Likes

```
function foo(){
  var arr = Array.prototype.slice.call( arguments );
  arr.push( "bam" );
  console.log( arr );
}
foo( "bar", "baz"); // ["bar","baz","bam"]
```
if slice() is called without any other parameters ==
the default values for its parameter have the effect of duplicating the `array`
Array.from(..) that can do the same task.
```
var arr = Array.from (arguments);
```
##  Strings

```
var a = "foo";
var b = ["f", "o", "o"];

a.length; // 3
b.length; // 3

a.indexOf("o"); // 1
b.indexOf("o"); //1

var c = a.concat("bar");  // "foobar"
var d = b.concat(["b", "a", "r"]); //[“f","o","o","b","a","r”

a === c;  // false
b === d;  // false

a; // "foo"
b; // ["f", "o", "o"]

```
`arrays` and `strings` both have
length property
`indexof()` method
`concat()` method
`string` are immutable;
`array` are mutable

consequence of immutable `string`s is that none of the `string` methods that alter its contents can modify in-place, but rather must create and return new `string`s.
Many of the array methods that can change array contents actually do modify in-place:

```
c = a.toUpperCase();
a === c; // false
a;       // "foo"
c;       // "FOO"

b.push( "!" );
b;  // ["f","o", "o", "!"]
```
many of the `array` methods that could be helpful when dealing with `string`s are not actually available for them”

```
a.join; // undefined
a.map;  // undefined

var c = Array.prototype.join.call( a, "-");
var d = Array.prototype.map.call(a, function(v){
  return v.toUpperCase() + '.';
  }).join( "" );

c; // "f-o-o"
d; // "F.O.O"
```
reverse a string

```
var c = a.split("").reverse().join("");

c; //"oof"
```
##  Numbers

Very  large or small `numbers` will by default be outputted in exponent form， method => toExponential()

```
var a = 5E10;
a;  // 50000000000
a.toExponential(); //"5e+10"

var b = a * a;
b;                // 2.5e+21

var c = 1 /a;
c;                //2e-11
```

`number` values can be boxed with the  `Number` object wrapper, `number` values can access methods that are built into the  `Number.prototype`. For example, the  `toFixed()` method allows you to specify how many fractional decimal places you'd like the value to be represented with:

```
var a = 42.59;

a.toFixed( 0 );//"43"
a.toFixed( 1 );//"42.6"
a.toFixed( 2 );//"42.59"
a.toFixed( 3 );//"42.590"
a.toFixed( 4 );//"42.5900"
```
the output is actually a string;
`toPrecision()` is similar.
```
var a =42.59

a.toPrecision( 1 );  //"4e+1"
a.toPrecision( 2 );  //"43"
a.toPrecision( 3 );  //"42.6"
a.toPrecision( 4 );  //"42.59"
a.toPrecision( 5 );  //"42.590"
a.toPrecision( 6 );  //"42.5900"
```

```
// invalid syntax;
42.toFixed( 3 ); //syntaxError

// these are all valid:
(42).toFixed( 3 ); //"42.000"
0.42.toFixed( 3 ); //"0.420"
42..toFixed( 3 ); //"42.000"
42 .toFixed( 3 ); //"42.000"
```

```
var onethousand = 1E3;  // means 1 * 10^3
var onemilliononehuandredthousand = 1.1E6 // means 1.1 * 10^6
```
numbers literal can also be expreassed in other bases, like binary, octal, hexadecimal.

```
0xf3; // hexadecimal for:243
0xf3; //ditto

0363; //octal for:243
```

#### Small Decimal Values

```
0.1 + 0.2  === 0.3;  // false
```
why????
the representation for 0.1 and 0.2 in binary floating point are not exact, so when they are added, the result is not exactly 0.3. Its really close 0.30000000000000004. but if your comparision fails,"close"  is irrelevant.


#### Testing for Integers

Number.isInteger()

```
Number.isInteger( 42 ); // true
Number.isInteger( 42.000 ); //true
Number.isInteger( 42.3 ) ; //false

if(!Number.isInteger) {
    Number.isInteger = function(num) {
        return typeof num == "number" && num % 1 == 0;
    };
}
```
to test if a value is a safe integer, use the ES6-specified Number, `isSafeInteger()`;
```
Number.isSafeInteger(Number.MAX_SAFE_INTEGER); //true
Number.isSafeInteger(Math.pow(2, 53));  //false
Number.isSafeInteger(Math.pow(2, 53) - 1) //true;

if(!Number.isSafeInteger) {
    NUmber.isSafeInteger = function(num) {
        return Number.isInteger(num) && Math.abs(num) <= Number.MAX_SAFE_INTEGER;
    };
}
```
#### 32-Bit (Signed) Integers


## Special Values


#### The Nonvalue Values

* `null` is an empty value
* `undefined` is a missing value

or
* `undefined` hasnt had a value yet
* `null` had a value and doesn't anymore


#### undefined

```
function foo() {
    undefined = 2; //really bad idea!
}
foo();

function foo() {
    "use strict";
    undefined = 2; //TypeError!
}
foo();

//it works, but its a terrible idea!

function foo() {
    "use strict";
    var undefined = 2;
    console.log(undefined); //2
}
foo();
```

#### void operator

The expression `void` ____"voids" out any value, so that the result of the expression is always the `undefined` value.
```
var a = 42;
console.log( void a, a); //undefined 42
```
但是 `void` 操作在一定情况下是有用的，如果你确定表达式没有结果值。
例如：
```
function doSomthing() {
    //note: `App.ready` is provided by our application
    if(!App.ready) {
        //try again later
        return void setTimeout( doSomthing, 100);
    }
    var result;
    // do some other stuff
    return result;
}
// were we able to do it right away?
if(doSomthing()){
    //handle next tasks right away
}
```


```
if(！APP.ready) {
    //try again later
    setTimeout (doSomthing, 100);
    return;
}
```
如果有时候你发现表达式里的一个值是存在的，并且你发现假如这个值是`undefined`是有用的，那使用`void`运算符

#### Special Numbers
##### The not number,numbers
NaN literally stands for “not a number”.尽管这个说法不准确
更准确的应该说 NaN is an "invalid number"(无效的数字)，"failed number"(错误的数字), "bad number"(坏的数字)。

```
var a = 1/"foo"; // NaN
typeof a == "number";  //true
```

"the type of not-a-number is `number`"
or "the type of NaN is `number`"
`NaN` 是数字类型
非数字 是数字类型

```
var a = 2/ "foo";
a  == NaN;  //false
a === NaN;  //false
NaN !== NaN //true
isNaN(a); //true 是不是非数字
```
`NaN` 是一个特殊的值，它永远不会等价于另外一个`NaN`(就是说它永不等于它自己)
```
var a = a /"foo";
var b = "foo";

a; //NaN
b; "foo"

window.isNaN( a ); //true
window.isNaN( b );// true -- ouch!
```
"foo"很显然不是数字，但是也不是非数字。这是js的bug。
ES6 使用新的工具 `NUmber.isNaN()`
```
if(!Number.isNaN) {
    Number.isNaN = function(n) {
        return(
            typeof n === "number" && window.isNaN( n )
            );
    };
}

var a = 2 /"foo";
var b= "foo";

Number.isNaN( a ); //true
Number.isNaN( b ); //false
```
其实我们是可以利用非数字的特点

```
if(!Number.isNaN) {
    Number.isNaN = function(n) {
        return n! = n;
    };
}
```
> 总结 使用 `isNaN`是有bug, ES6使用了新的工具 Number.isNaN

#### infinity（无穷数)

Infinity / Infinity is not a defined operation. In JS, this results in NaN.
无穷数除以无穷数结果是 NaN(非数字)
finite / Infinity = 0

#### Zeros
```javascript
var a =0;
var b = 0 / -3;

a == b;  //true
-0 == 0; //true

a === b; // true
-0 === 0; //true

0 > -0;  //false
a > b; //false
```
如果你想要区别 0 和 -0

```javascript
function isNagZero(n) {
    n =Number(n);
    return (n===0) && (1/n === -Infinity);
}

isNagZero( -0 ); //true
isNagZero( 0 / -3 );//true
isNagZero( 0 );//false
