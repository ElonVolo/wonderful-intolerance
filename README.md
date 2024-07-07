# wonderful-intolerance
A wonderfully intolerant code style that produces wonderfully wonderful projects.

## Preface

The most important traits for a code style: is that other people find it wonderfully understable, wonderfully debuggable, and that it wonderfully discourages people from doing unwonderful things in an attempt to make themselves look wonderfully clever.

## Spec

### No tail calls

Bad
```
  function foo() {
    return bar();
  }
```

Good
```
  function foo() {
    let result = bar();
    return bar;
  }
```

Rationale: debugger-friendly.

### Unary returns only
Bad
```
  function addTwoValues(fooValue, barValue) {
    return fooValue + barValue;
  }
```

Good
```
  function addTwoValues = foo(fooValue, barValue) {
    let addedValue = fooValue + barValue;
    return addedValue;
  }
```

Rationale: debugger-friendly.





### No compound indexs
Bad
```
    let myElement[foo + calculateBar());
```

Good
```
    let barValue = calculateBar();
    let myElementIndex = barValue + foo;
    let myElement = myArray[myElementIndex];
```

Good
```
    let myElementIndex = foo + bar;
    let myElement = myArray[myElementIndex]
```
    
### No binary expressions in function parameters
Bad
```
    function foo(i, mystuff() + j, whatever) {

    }
```

Bad
```
  myFunction(5, foo + bar) {
    whatever();
  }
```

Bad
```
  myFunction(5, checkValue(foo)) {
    whatever
  }
```

Good
```
      myFunction(5, foo) {
      let checkResult = checkValue(foo);
      whatever()
  }
```

### Never rely on order of evaluation and precedence

Rationale:

Relying on order of evaluation:

- Creates more effort to understand
- More chance for human error
- Less experiened developers might get it wrong
- Invites cleverness that violates Kernighan's Law.


### No magic numbers

Rationale: hurts meaning.

Exception: extraordinarily obvious things that are universally known constants.

```
    // This could e excessive.
    let myHalfValue = myValue / 2 is excessive.
```


### Semicolons always

Bad
```
   let myValue = myFunc
   let baz = foo + bar
```

Good
```
   let myValue = myFunc;
   let baz = foo + bar;
```

Rationale:

* Repetition and consistency.
* In languages where a lack of semicolons could cause an issue, it's better to error on the side of safety.

Exception: if you're dealing with a language that doesn't use them or it's so customary to not use a semicolon it's absurd (python, ruby)


### Optional means "Required 100% of the time"



### Tabs not spaces

Rationale: accessibility issues

### No inline comments

Rationale

- Repetition and consistency.
 
### No nested ternaries

- Creates more effort to understand.
- More chance for human error.
- Invites cleverness that violates Kernighan's Law.

### No calling functions in nested ternaries

Bad
```
			const newNodes =
				(typeof insert === 'function') ? insert.call(path, path, i) : insert;
			path.insertBefore.apply(path, toArray(newNodes));
```

Good
```
			const newNodes =
				(typeof insert === 'function') ? insert.call(path, path, i) : insert;
			path.insertBefore.apply(path, toArray(newNodes));
```

### No global variables

Exception: an exceptionally good reason

### No fat arrow implicit returns

Bad
```
  let myValue = map(x => x + myValue);
```

Good
```
   let myValue = map(x => {
      let addedValue = x + myValue;
      return addedValue;
   };
```

Rationale:

- Debugger-friendly
- There can be misunderstandings about the implicit returns.

### No one line branching statements

Bad
```
  if (!scope) return;
```

Good
```
  if (!scope) {
    return;
  }
```

Rationale:

Rationale:

- Debugger friendly.
- Easier to visual scan and tell riht away it's a branch.

### No function chaining

Bad
```
  foo().bar();
```

Good
```
  let resultObject = foo();
  resultObject.bar();
```

Rationale:

- Debugger friendly.

### No nested ternaries

Rationale:

- Debugger friendly.
- Hard to read, especially when taken to extremes.

### No calling functions in function parameters

Bad
```
  function lookupUserInfo(userID, getUserTable()) {
    // whatever
  }
```

Good
```
  function lookupUserInfo(userID, userTable) {
    // Whatever
  }

  let userLookupTable = getUserTable();
  lookupUserInfo(userID, userLookupTable);
```

Rationale:

- Debugger friendly.
- Nesting is for the birds.

### Always used named exports

Rationale:
- Repetition and consistancy and repetition and consistency and repetition and consistency.

Bad:

```
export class Foo {

}
```

Good

```
class Foo {

}

export { Foo };
```

### All parameters have types
#### TODO: stop looking a hypocrite an make sure all my examples have type annotatinos

Bad:
```
function sayHello(name) {
  console.log("Hello " + name);
}
```

Good:

```
function sayHello(name: string) {
   console.log("Hello " + name);
}
```

Rationale:

- In most cases developers should be allowed to know what exactly what's being passed to a parameter

### No index chanining

Bad
```
  const bindings = scope.getBindings()[name];
```

Good
```
  const bindings = scope.getBindings()
  let binding = bindings[name];
```

Rationale:

- Debugger friendly.

