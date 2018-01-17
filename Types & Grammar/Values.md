# Values

## Arrays
 containers for any type of Value

```
var a = [1, "2", [3]];

a.length; // 3
a[0] === 1; //true
a[2][0] === 3 // true
```

```
var a =[];

a.length; // 0
a[0] = 1;
a[1] = "2";
a[2] = [3];

a.length; // 3
```

```
var  a = []

a[0] = 1;
// no 'a[1]' slot set here
a[2] = [3];
a[1]; // undefined

a.length; //3
```
arrays also are objects

```
var a = [];

a[0] = 1;
a["foobar"] = 2;

a.length;    // 1
a["foobar"]; // 2
a.foobar     // 2
```
a `string` value intented as a key can be coerced to a standard base 10 `number`.

```
var a = [];
a["13"] = 42;
a.length; //14
```

## Array-Likes

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
## Strings

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
## Numbers
