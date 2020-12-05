# A list of Javascript Gotchas

## Floating Points

Javscript cannot represent 0.1 and 0.2 accurately.

```
0.1 + 0.2 !== 0.3
```

it actually evaluates to `0.30000000000000004`

---

## null

1. The typeof `null` is an object
2. Unitialized variables have a default value of `undefined` rather than `null`

---

## Comparing Objects

Javascript objects are compared by reference (an address in memory).  
So two objects with the same properties and values will not necessarily be equal.

```
const a  = { value: 5 }
const b = { value: 5 }

a === b // false
```

compared with

```
const c = a
a === c // true
```

This is why you shouldn't put objects in the `React.useEffect` dependency array.  
Lodash has an `isEqual` function for deep comparisons.

---

## false

`[], 0, ''` all evalutes to false

---

## forEach

1. Returns undefined
2. Will not work as expected for for an async / await (won't wait for the return value)

```
const people = [ 'Mane' ,'Salah', 'Firmino' ]

async function getPictures(){
    people.forEach(async (person) => {
        const goals = await fetch(person)
        console.log(goals)
    })
}
```

---

## Switch

[Block-scope variable within switch statement](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/switch)

If you want to use the same variable name in different case clauses, you need to wrap the whole clause with brackets

```
switch (animal) {
  case 'dog': {
    let warning = 'this is dog'
    console.log(warning)
    break
  }
  case 'cat': {
    let warning = 'this is cat'
    console.log(warning)
    break
  }
}
```

### Omitting the break / return statement

A switch statement will run from the matched case until it encounters a break statement (regardless of whether the cases match)

```
const animal = 'dog'

switch (animal) {
  case 'dog': {
    let warning = 'this is dog'
    console.log(warning)
  }
  case 'cat': {
    let warning = 'this is cat'
    console.log(warning)
    break
  }
}
```

This will run both the dog and cat cases

---

## NaN

### [source: Stephen Hartfield](https://www.digitalocean.com/community/tutorials/js-gotchas)

```
**anything in the JavaScript universe** === NaN // false
```

There are no exceptions

```
NaN ===  NaN // false
NaN == NaN // false
```

### isNaN is also weird

```
isNaN("name"); // true
isNaN(123); // false

isNaN(""); // false
isNaN("45"); // false - this is a string, I thought
isNaN([]); // false - wait so an empty array is a number?

isNaN([1, 2]); // true
isNaN({}); // true
isNaN(() => {}); // true
```

---

## Equality / Truthy vs Falsy

### [source: Stephen Hartfield](https://www.digitalocean.com/community/tutorials/js-gotchas)

```
false == '0' // true
0 == false   // true
'' == 0      // true
false == ''  // true
[] == ''     // true, but we'll get to this

'1' == true  // true
1 == true    // true
'false' == true // true
```

---

## Number Constructor

```
Number(undefined) // NaN
Number(null) // 0
```
# javascript-gotchas
