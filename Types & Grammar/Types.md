## Build-in Types (内置类型)

JavaScript defines seven built-in Types

* null
* underfined
* boolean
* number
* string
* object
* symbol - added in ES6!

All of these types except object are called "primitives".

```
typeof underfined   === "underfined";   // true
typeof true         === "boolean";      // true
typeof 42           === "number";       // true
typeof "42"         === "string";       // true
typeof { life: 42}  === "object";       // true
typeof Symbol()     === "symbol";       // true

typeof null   === "object";    //true

```

if you want to test for  a null value using its type, you need to a compound condition:

```
 var a = null;
 (!a && typeof a === "object"); // true
typeof function a() { /* .. */ } === "function";  //true
```

the functions are actually objects us quite useful.Most importantly, they can have properties. 例如

```
function a(b, c){
     /* .... */
}
```
函数对象有长度属性   成正式参数数字

```
a.length; //2

```
既然你宣称函数带有两个正式参数（b and c),这个函数的长度就是 2.
那么数组呢？他们是原生的JS,因此他们有特别的类型？

```
 typeof [1,2,3] === "object"; //true

```
不，只是对象。更真确的是认为他们是 对象的子类型，

## Values as Types (值和类型)

在JavaScript, 变量没有类型， 值有类型，变量在任何时候获得任何类型。

另一种方法思考Js类型就是：Js没有类型强行机制，一个变量可以在一个赋值中获得`string`,在下一次赋值中获得`数字`类型，等等。

值42有`nummber`固有类型,但是他类型可以改变，另一个值 `'42'`有字符串类。
如果你使用 `typeof` 在一个变量之前，
它不是问： 这个变量是什么类型？
它是问：在这个变量中是什么类型的值？

```
var a = 42;
typeof a; // 'number'

a = true;
typeof a; // 'boolean'

typeof typeof 42; // "string"

```
第一个 typeof 42 返回 `"number"`, 那么 typeof `number` 是 `string`。

## underfined Versus "undeclared" (无定义的 和 没有声明的)

```
var a;
typeof a; //"undefined"

var b = 42;
var c;

// later

b = c;
typeof b; // "underfined"
typeof c; // "underfined"

```
> **提示**  `underfined` 变量是在可以到达的作用域里被声明，但是在那一刻没有值在这个变量里。
 相反 `undeclared` 是没有被声明的变量是，在一个可以通过的作用域内，没有被正式声明。

```
var a;
a; // underfined
b; // ReferenceError: b is not defined
```
a: 'underfined'
b: 'undeclared'

```
var a;
 typeof a; // "underfined"
 typeof b; // "underfined"
```
still
a: 'underfined'
b: 'undercaled'

#### type of Undercaled(未声明的类型)

```
// oops, this would throw an error!
if(DEBUG) {
    console.log("Debugging is starting");
}

// this is a safe existence check
if(typeof DEBUG !== "underfined") {
    console.log("Debugging is starting");
}

```
这样的检查是非常有用的如果你不是处理用户定义的变量
如果你对一个内置API即将检验，你可以会发现这个对检验是有用处的，不会导致错误

```

if( typeof atob === "underfined") {
    atob = function() {
        /* ... */
    };
}
```
> **注意**

检测全局变量的另外一个方法，但不需要用安全护卫功能`typeof`

```
if(window.DEBUG) {
    //..
}

if(!window.atob){
    //..
}
```

但是，手动引用全局变量window引用是一些开发人员喜欢避免的，尤其是你的代码需要在多种js环境下运行（不仅仅是浏览器，还有服务器端node.js)这些全局变量可能不会总是window.

例如，你有一个函数，别人需要copy -paste到他们程序里面去，在此你想要检测是否有一些变量已经定义了。
```
function doSomthingCool(){
    var helper =
        (typeof FeatureXYZ !== "underfined") ？
        FeatureXYZ:
        function(){ /*.. default feature ..*/};
    var val = helper();
    // ..
}

```
doSomthingCool() 这个函数检测变量 FeatureXYZ是否存在,如果找到这个变量，就使用它，如果没有，使用它自己的函数。现在如果一个人想包含`FeatureXYZ()`到自己的程序里，最安全的方法是检测是否他之前已经定义了`FeatureXYZ`

```
// an IIFE (see the "Immediately Invoked Function Expressions"
// discussion in the Scope & Closures title in this series)
(function(){
    function FeatureXYZ() { /*..my XYZ feature..*/}

    // include 'doSomthingCool(...)'
    function doSomthingCool(){
        var helper =
            (typeof FeatureXYZ !== "underfined") ？
            FeatureXYZ:
            function(){ /*.. default feature ..*/};
        var val = helper();
        // ..
    }
    doSomthingCool();

})();

```
Here, FeatureXYZ is not at all a global variable, but we’re still using
the safety guard of typeof to make it safe to check for.  最重要的是我们没有使用(`window._`)来检测，所以 `typeof`是非常有用的。

还有一些程序员喜欢用"`dependency injection`"

```
function doSomthingCool(FeatureXYZ) {
     var helper = FeatureXYZ ||
    function(){ /*.. default feature ..*/ };

    var val = helper();
    //
}

```
#### 总结

JavaScript 有7中类型：`null`, `object`, `boolean` `undefined`,`string`,`number`,`symbol`.

变量没有类型，变量的值是有类型的。

`undefined` 和 `undeclared`，非定义和 非声明是不一样的。
`Undeclared` 表示一个变量没有被声明。
对于它们的 `typeof`返回值都是 '`undefined`'
