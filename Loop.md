## loop
---
``` javascript

while ( numOfCustomers > 0 )  {
  console.log(" How may I help you? ");
  numofCustomers = numOfCustomers  - 1;
}

// versus

do {
  console.log(" How may I help you? ");
  numofCustomers = numOfCustomers  - 1;
} while (numOfCustomers > 0);

```
> If the condition is initially false, a while loop will never run, but a do..while loop will run just the first time.


null bug
---
```javascript

a = null;
typeof a;

// "object" -- weird, bug
```

Truthy & Falsy
---

falsy
---

* "" (empty string)
* 0, -0, NaN (invalid number)
* null, undefined
* false

Truthy
---

* “hello"
* 42
*  [],[1, "2",3]  (arrays)
* { }, {a: 42} (objects)
* function foo() {...} (functions)