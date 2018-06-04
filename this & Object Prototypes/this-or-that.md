## this or That ?


### why this ?

```javascript
function identify() {
  return this.name.toUpperCase();
}

function speak() {
  var greeting = "Hello, I'm " + identify.call( this );
  console.log( greeting );
}

var me = {
  name: "Kyle"
};

var you = {
  name: "Reader"
};

identify.call( me );
identify.call( you );

speak.call( me );
speak.call( you );
```

```javascript
function identify(context) {
  return context.name.toUpperCase();
}

function speak(context) {
  var greeting = "Hello, I'm " + identify( context );
  console.log(greeting);
}

identify( you );
speak( me );
```

## Confusions

### Itself

```javascript

function foo(num) {
  console.log( "foo: " + num );
  this.count++;
}

foo.count = 0;

var i;
for (i=0; i<10; i++){
  if (i >5) {
    foo( i );
  }
}

console.log( foo.count );
```

注意：
> `this` is not in fact pointing at all to that function object, and so even though the property names are the same, the root objects are different, and confusion ensues.
>
> `this` 并不是指向函数本身，尽管属性名是一样的，但是根对象并不一样。

```javascript

function foo(num) {
  console.log( "foo: " + num );
  data.count++;
}

var data = {
  count: 0
};

var i;

for (i=0; i<10; i++) {
  if (i > 5) {
    foo( i );
  }
}

// foo: 6
// foo: 7
// foo: 8
// foo: 9

// how many times was 'foo' called?
console.log(data.count);

```

```javascript
function foo(num) {
  console.log( "foo: " + num );
  foo.count++;
}

foo.count = 0;

var i;

for (i=0, i<10; i++) {
  if (i > 5) {
    foo( i );
  }
}
// foo: 6
// foo: 7
// foo: 8
// foo: 9

// how many times was 'foo' called?

console.log( foo.count );
```
>another way of approaching the issue is to force this to actually point at the foo function object:
另外一个接近问题的方法就是强迫`this`指向函数。

```javascript
function foo(num) {
  console.log( "foo: " + num);
  this.count++;
}

foo.count = 0;
var i;

for (i=0; i<10: i++) {
  if (i > 5) {
    foo.call(foo, i);
  }
}
// foo: 6
// foo: 7
// foo: 8
// foo: 9

// how many times was `foo` called?
console.log( foo.count );
```
### Its Scope

```javascript
function foo() {
  var a = 2;
  this.bar();
}

function bar() {
  console.log (this.a)
}

foo();
```
## Whats this?

>`this` is actually a binding that is made when a function is invoked, and what it references is determined entirely by the call-site where the function is called.
`this`实际上是一个绑定，当一个函数被调用时产生，它所引用的内容完全由调用该函数的调用站点决定。