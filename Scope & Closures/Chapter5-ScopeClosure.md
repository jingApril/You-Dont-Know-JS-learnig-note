## Loops + Closure

```javascript

    for (var i=1; i<=5; i++) {
        setTimeout ( function timer() {
            console.log( i );
        }, i* 1000 );
    }

    for (var i=1; i<=5; i++) {
        (function(){
            setTimeout ( function timer(){
                console.log( i );
            }, i*1000 );
        })();
    }

    for (var i=1; i<=5; i++) {
        (function(){
            var j = i;
            setTimeout( function timer(){
                console.log(i);
            }, j*1000)
        })();
    }

    for (var i=1; i<=5; i++){
        (function(j){
            setTimeout( function timer(){
                console.log(j);
            }, j*1000)
        })(i)
    }
```
### Block Scoping Revisited

```javascript

    for (var i=1; i<=5; i++) {
        let j = i;
        setTimeout( function timer(){
            console.log( j );
        }, j*1000);
    }

    for (let i=1; i<=5; i ++) {
        setTimeout( funtion timer(){
            console.log( i );
        }, i*1000 );
    }

```
## Modules

```javascript

    fucntion foo(){
        var something = "cool";
        var another = [1, 2, 3];

        function doSomething() {
            console.log( something );
        }

        function doAnother() {
            console.log( another.jpon("!"));
        }
    }

    function CoolModule() {
        var something = "cool";
        var another = [1, 2, 3];

        function doSomething() {
            console.log( something );
        }

        function doAnother() {
            console.log( another.join("!"));
        }
        return {
            doSomething: doSomething,
            doAnother: doAnother
        }
    }
    var foo = CoolModule();

    foo.doSomething();
    foo.doAnother();

    // another way

    var foo = (function CoolModule() {
        var something = "cool";
        var another = [1, 2, 3];

        function doSomething() {
            console.log( something );
        }

        function doAnother() {
            console.log( another.join("!"));
        }

        return {
            doSomthing: doSomthing,
            doAnother: doAnother
        };
    })();

    foo.doSomthing(); // cool
    foo.doAnother(); // 1 ! 2 ! 3

    //Modules can receive parameters

    function CoolModule(id) {
        function identify() {
            console.log( id );
        }

        return  {
            identify: identify
        };
    }

    var foo1 = CoolModule( "foo 1" );
    var foo2 = CoolModule( "foo 2" );

    foo1.identify(); // "foo 1"
    foo2.identify(); // "foo 2"

    // name the object you are returning as your public API

        var foo = (function CoolModule(id) {
            function change() {
                // modifying the public API
                publicAPI.identify = identify 2;
            }

            function identify1() {
                console.log( id );
            }

            function identify2() {
                console.log( id.toUpperCase() );
            }

            var publicAPI = {
                change: change,
                identify: identify1
            };

            return publicAPI;
        })( "foo module" );

foo.identify(); // foo module
foo.change();
foo.identify(); // FOO MODULE

```
## Modern Modules

```javascript
 var MyModules = (function Manager(){
     var modules = {};

     function define(name, deps, impl) {
         far (var i =0; i<deps.length; i++) {
             deps[i] = modules[deps[i]];
         }
         modules[name] = impl.apply(impl, deps);
     }

     function get(name) {
         return modules[name];
     }

     return {
         define: define;
         get: get
     };
 })();
```
