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

### No global variables

Exception: an exceptionally good reason

### No fat arrow implicit returns

