---
title: Top 10 ES6 features by example
date: 2017-11-28 22:27:23
tags:
---


## [Top 10 ES6 features by example](https://blog.pragmatists.com/top-10-es6-features-by-example-80ac878794bb)


Summary


### 1. const and let keywords

- `var` have function scope and are hoisted to the top.
- `let` and `const` have block scope (surrounded by `{}`)

```js
function f() {
  var x = 1
  let y = 2
  const z = 3
  {
    var x = 100
    let y = 200
    const z = 300
    console.log('x in block scope is', x)
    console.log('y in block scope is', y)
    console.log('z in block scope is', z)
  }
  console.log('x outside of block scope is', x)
  console.log('y outside of block scope is', y)
  console.log('z outside of block scope is', z)
}

f()
```

Result:

```js
x in block scope is 100 
y in block scope is 200 
z in block scope is 300 
x outside of block scope is 100 
y outside of block scope is 2 
z outside of block scope is 3 
```


### 2. Array helper functions

#### `forEach`

- just iterate, `undefined` return.

```js

var colors = ['red', 'green', 'blue']

function print(val) {
  console.log(val)
}

colors.forEach(print)
```

Result:

```js
red 
green 
blue 
```

#### `map`

- returns a new `array` with same number of elements

```js
var colors = ['red', 'green', 'blue']

function capitalize(val) {
    return val.toUpperCase()
}

var capitalizedColors = colors.map(capitalize)

console.log(capitalizedColors)
```

Result:

```js
["RED","GREEN","BLUE"] 
```

#### `filter`

- returns a new `array` filtered.

```js
var values = [1, 60, 34, 30, 20, 5]

function lessThan20(val) {
    return val < 20
}

var valuesLessThan20 = values.filter(lessThan20)

console.log(valuesLessThan20)
```

Result:

```js
[1,5] 
```

#### `find`

- returns the first matched element **or** `undefined`

```js
var people = [
  {name: 'Jack', age: 50},
  {name: 'Michael', age: 9}, 
  {name: 'John', age: 40}, 
  {name: 'Ann', age: 19}, 
  {name: 'Elisabeth', age: 16}
]

function teenager(person) {
    return person.age > 10 && person.age < 20
}

var firstTeenager = people.find(teenager)

console.log('First found teenager:', firstTeenager.name)
```

Result:

```js
First found teenager: Ann 
```

#### `every`

- Checks if every element of the array passes the test implemented by the provided function, which should return `true` or `false`.

```js
var people = [
  {name: 'Jack', age: 50},
  {name: 'Michael', age: 9}, 
  {name: 'John', age: 40}, 
  {name: 'Ann', age: 19}, 
  {name: 'Elisabeth', age: 16}
]

function teenager(person) {
    return person.age > 10 && person.age < 20
}

var everyoneIsTeenager = people.every(teenager)

console.log('Everyone is teenager: ', everyoneIsTeenager)
```

Result:

```js
Everyone is teenager:  false 
```

#### `some`

- Checks if any element of the array passes the test implemented by the provided function, which should return true or false.

```js
var people = [
  {name: 'Jack', age: 50},
  {name: 'Michael', age: 9}, 
  {name: 'John', age: 40}, 
  {name: 'Ann', age: 19}, 
  {name: 'Elisabeth', age: 16}
]

function teenager(person) {
    return person.age > 10 && person.age < 20
}

var thereAreTeenagers = people.some(teenager)

console.log('There are teenagers:', thereAreTeenagers)
```

Result:

```js
There are teenagers: true 
```

#### `reduce`

- Applies a function passed as the first parameter against an accumulator and each element in the array (from left to right), thus reducing it to a single value. The initial value of the accumulator should be provided as the second parameter of the reduce function.

```js
var array = [1, 2, 3, 4]

function sum(acc, value) {
  return acc + value
}

function product(acc, value) {
  return acc * value
}

var sumOfArrayElements = array.reduce(sum, 0)
var productOfArrayElements = array.reduce(product, 1)

console.log('Sum of', array, 'is', sumOfArrayElements)
console.log('Product of', array, 'is', productOfArrayElements)
```

Result:

```js
Sum of [1,2,3,4] is 10 
Product of [1,2,3,4] is 24 
```

### 3. Arrow functions

- functions with inherited scope

```js
var array = [1, 2, 3, 4]

const sum = (acc, value) => acc + value
const product = (acc, value) => acc * value

var sumOfArrayElements = array.reduce(sum, 0)
var productOfArrayElements = array.reduce(product, 1)
```

inline:

```js
var array = [1, 2, 3, 4]

var sumOfArrayElements = array.reduce((acc, value) => acc + value, 0)
var productOfArrayElements = array.reduce((acc, value) => acc * value, 1)
```

complex:

```js
var array = [1, 2, 3, 4]

const sum = (acc, value) => {
  const result = acc + value
  console.log(acc, ' plus ', value, ' is ', result)
  return result
}

var sumOfArrayElements = array.reduce(sum, 0)
```

### 4. Classes

- syntactic sugar for prototypal inheritance.

```js
class Point {
    constructor(x, y) {
        this.x = x
        this.y = y
    }

    toString() {
        return '[X=' + this.x + ', Y=' + this.y + ']'
    }
}

class ColorPoint extends Point {
    static default() {
        return new ColorPoint(0, 0, 'black')
    }

    constructor(x, y, color) {
        super(x, y)
        this.color = color
    }

    toString() {
        return '[X=' + this.x + ', Y=' + this.y + ', color=' + this.color + ']'
    }
}

console.log('The first point is ' + new Point(2, 10))
console.log('The second point is ' + new ColorPoint(2, 10, 'green'))
console.log('The default color point is ' + ColorPoint.default())
```

Result

```js
The first point is [X=2, Y=10] 
The second point is [X=2, Y=10, color=green] 
The default color point is [X=0, Y=0, color=black] 
```

### 5. Enhanced object literals

Object literals enhanced.
- define fields with variable assignment of the same name
- define functions
- define dynamic (calculated) properties

```js

const color = 'red'
const point = {
  x: 5,
  y: 10,
  color,
  toString() {
    return 'X=' + this.x + ', Y=' + this.y + ', color=' + this.color
  },
  [ 'prop_' + 42 ]: 42
}

console.log('The point is ' + point)
console.log('The dynamic property is ' + point.prop_42)
```

Result:

```js
The point is X=5, Y=10, color=red 
The dynamic property is 42 
```

### 6. Template strings

- multi-line text too

```js
function hello(firstName, lastName) {
  return `Good morning ${firstName} ${lastName}! 
How are you?`
}

console.log(hello('Jan', 'Kowalski'))
```

Result:

```js
Good morning Jan Kowalski! 
How are you? 
```

### 7. Default function arguments

```js
function sort(arr = [], direction = 'ascending') {
  console.log('I\'m going to sort the array', arr, direction)
}

sort([1, 2, 3])
sort([1, 2, 3], 'descending')
```

Result:

```js
I'm going to sort the array [1,2,3] ascending 
I'm going to sort the array [1,2,3] descending 
```

### 8. Rest and spread operators

It enables extraction of array or object content as single elements.


#### `Spread`

Example — make shallow copy of array:

```js
var array = ['red', 'blue', 'green']
var copyOfArray = [...array]

console.log('Copy of', array, 'is', copyOfArray)
console.log('Are', array, 'and', copyOfArray, 'same?', array === copyOfArray)
```

Result

```js

Copy of ["red","blue","green"] is ["red","blue","green"] 
Are ["red","blue","green"] and ["red","blue","green"] same? false 
```

Example — merge arrays:

```js
var defaultColors = ['red', 'blue', 'green']
var userDefinedColors = ['yellow', 'orange']

var mergedColors = [...defaultColors, ...userDefinedColors]

console.log('Merged colors', mergedColors)
```

Result

```js
Merged colors ["red","blue","green","yellow","orange"] 
```

#### `Rest`

- spread in function parameters

```js
function printColors(first, second, third, ...others) {
  console.log('Top three colors are ' + first + ', ' + second + ' and ' + third + '. Others are: ' + others)
}
printColors('yellow', 'blue', 'orange', 'white', 'black')
```

Result

```js
Top three colors are yellow, blue and orange. Others are: white,black 
```

### 9. Destructuring

#### Destructuring array

Enables extraction of requested elements from the array and assigning them to variables.

```js
function printFirstAndSecondElement([first, second]) {
    console.log('First element is ' + first + ', second is ' + second)
}

function printSecondAndFourthElement([, second, , fourth]) {
    console.log('Second element is ' + second + ', fourth is ' + fourth)
}

var array = [1, 2, 3, 4, 5]

printFirstAndSecondElement(array)
printSecondAndFourthElement(array)
```

Result 

```js
First element is 1, second is 2 
Second element is 2, fourth is 4 
```

#### Destructuring object

Enables extraction of requested properties from the object and assigning them to variables of the same name as properties.

```js
function printBasicInfo({firstName, secondName, profession}) {
  console.log(firstName + ' ' + secondName + ' - ' + profession)
}

var person = {
  firstName: 'John',
  secondName: 'Smith',
  age: 33,
  children: 3,
  profession: 'teacher'
}

printBasicInfo(person)
```

Result 

```js
John Smith - teacher 
```

### 10. Promises

```js
function asyncFunc() {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
          const result = Math.random();
          result > 0.5 ? resolve(result) : reject('Oppps....I cannot calculate')
        }, 1)
    });
}

for (let i=0; i<10; i++) {
  asyncFunc()
      .then(result => console.log('Result is: ' + result))
      .catch(result => console.log('Error: ' + result))
}
```

Result

```js

Result is: 0.7930997430022211 
Error: Oppps....I cannot calculate 
Result is: 0.6412258210597288 
Result is: 0.7890325910244533 
Error: Oppps....I cannot calculate 
Error: Oppps....I cannot calculate 
Result is: 0.8619834683310168 
Error: Oppps....I cannot calculate 
Error: Oppps....I cannot calculate 
Result is: 0.8258410427354488 
```