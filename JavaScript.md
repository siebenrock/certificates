# Introduction

- Chrome Developer Tools, go to Console, enter JavaScript code
- Browser include JavaScript engines
- Can be used to test new code snippets
- Use Shift + Return to enter multiple lines of code
- `alert("Hello!")`
- `console.log("Hiya friend!");`
- Semicolon after at end of each line
  - Multiple lines of code can be written in same line

```
for (var i = 0; i < 10; i++) {
  console.log(i);
}
```

```
document.getElementsByTagName("h1")[0].style.color = "#ff0000";
```

# Data Types And Variables

## Comments

- Any text after `//`
- Any text in between `/*` and `*/` for block of comments

## Strings

- Use ' or "
- Concatenation by `"Hello" + " New York City"`

## Variables

- `var variableName = value;`
- `var greeting = "Hello";` for example
- Write name of variable using camelCase

## Indexing

- `"James"[0];` returns "J"
- First character starts at position zero

## Escaping Characters

- Use backslash to escape other characters
- Ignores characters special meaning and uses literal value of character
- `"The man whispered, \"please speak to me.\""` to have quotes inside string
- Special characters that need to be escaped
  - // for backslash
  - /" for double quote
  - /' for single quote
  - /n for newline
  - /t for tab

## Comparisons

- Use `==` and `!=` for equal comparisons for numbers and strings
- `"green" > "Green"` returns true
- `"1" == 1` returns true (implicit type coercion)
- `0 == false` returns true (implicit type coercion)
- JavaScript is loosely typed language meaning less specific data types are needed
- Use script equality to check whether numbers, string or booleans are identical in type and value
- `"1" === 1` returns false
- `1 !== false` returns false

## Booleans

- `true` or `false`

## Other

- Data type "null" is value of nothing
- `var x = null;`
- Purposefully assigned value to nothing
- Data type "undefined" absence of value
- `var x; console.log(x);`
- If value is not assigned
- "NaN" is "Not-a-Number"

# Conditionals

## If/Else Statement

```
var weather = "sunny";

if (weather === "snow") {
  console.log("Bring a coat.");
} else if (weather === "rain") {
  console.log("Bring a rain jacket.");
} else {
  console.log("Wear what you have on.");
}
```

## Logical Operators

```
var colt = "not busy";
var weather = "nice";

if (colt === "not busy" && weather === "nice") {
  console.log("go to the park");
}
```

- `&&` for logical AND
- `||` for logical OR
- `!` for logical NOT
- `!(4 === 4)` returns false

## Truthy And Falsy

- List of all falsy values
- Boolean value `false`
- `null` type
- `undefined` type
- Number `0`
- Empty string ""
- Odd value `NaN`
- Value is truthy if note in list of falsy

## Ternary Operator

```
conditional ? (if condition is true) : (if condition is false)
```

```
var isGoing = true;
var color = isGoing ? "green" : "red";
console.log(color);
```

- Using `if(isGoing)` is same as using `if(isGoing === true)`
- Alternatively, using `if(!isGoing)` is same as using `if(isGoing === false)`
- Replaces conditional statement and handles variable assignment for `color`

## Switch Statement

```
switch (option) {
  case 1:
    console.log("You selected option 1.");
  case 2:
    console.log("You selected option 2.");
  case 3:
    console.log("You selected option 3.");
}
```

- Allows to chain multiple `else if` statements that are based on same value without using conditional statements
- ` (option === [value])` is replaced with `case` clause
- Add `break;` to each case clause to terminate switch statement
- Following example shows falling-through on purpose
  - `winner` is equal to 3
  - Returns `You've won a smartwatch and tickets to the circus.`

```
var prize = "";

switch (winner) {
  case 1:
    prize += "a trip for two to the Bahamas and ";
  case 2:
    prize += "a four piece furniture set.";
    break;
  case 3:
    prize += "a smartwatch and ";
  default:
    prize += "tickets to the circus.";
}

console.log("You've won " + prize);
```

# Loops

## While Loop

```
var start = 0;
while (start < 10) {
  console.log(start);
  start = start + 2;
}
```

- Information has to be specified ahead, before running while loop

## For Loop

```
for (var i = 0; i < 6; i = i + 1) {
  console.log("Printing out i = " + i);
}
```

- Information is specified inside for loop

## Increment And Decrement

- `x++` or `++x` is same as `x = x + 1`
- `x++` returns original value of x before it gets incremented
- `x--` or `--x` is same as `x = x - 1`
- `x += 3` is same as `x = x + 3`
- `x -= 6` is same as `x = x - 6`
- `x *= 2` is same as `x = x * 2`
- `x /= 5` is same as `x = x / 5`

# Functions

```
function reverseString(reverseMe) {
    var reversed = ""<
    for (var i = reverseMe.length -1; i >= 0; i--) {
        reversed =+ reverseMe[i]
    }
    return reversed;
}

console.log(reverseString("Julia"));
```

- `return` stops execution of function and returns value back to caller, if nothing is defined as value to be returned back then `undefined` is returned
- One function passed into another function is called "Callback"

## Scope

- "Global scope" if variable is defined globally
- "Function scope" if variable is defined within function
- When trying to access identifier, JavaScript Engine will first look in current function, if it doesn't find anything, it will continue to next outer function to see if it can find identifier there, it will keep doing this until it reaches global scope

## Shadowing

```
var x = 1;

function addTwo() {
  x = x + 2;
}

addTwo();
x = x + 1;
console.log(x);

// Returns 4.
```

```
var x = 1;

function addTwo() {
  var x = x + 2;
}

addTwo();
x = x + 1;
console.log(x);

// Returns 2.
```

## Hoisting

- Before any JavaScript is executed, all function declarations are hoisted to top of their current scope
- Meaning that functions can be called in script before they are declared
- JavaScript hoists function declarations and variable declarations to top of current scope
- Variable assignments are not hoisted

## Function Expressions

- Functions can be stored in variable, called function expression, anonymous function
- Function keyword no longer has name
- Function can be accessed through variable name
- All function declarations are hoisted and loaded before script is actually run, function expressions are not hoisted, since they involve variable assignment

```
var catSays = function(max) {
  var catMessage = "";
  for (var i = 0; i < max; i++) {
    catMessage += "meow ";
  }
  return catMessage;
};
```

```
// Anonymous function expression
var doSomething = function(y) {
  return y + 1;
};
```

```
// Named function expression
var doSomething = function addOne(y) {
  return y + 1;
};
```

```
// For either of definitions above, call function like this:
doSomething(5);
```

- Pass one function into another

```
function movies(messageFunction, name) {
  messageFunction(name);
}

movies(function displayFavorite(movieName) {
  console.log("My favorite movie is " + movieName);
}, "Finding Nemo");
```

# Arrays

- Data structure that can be used to store multiple values
- Sample arrays
  - `var donuts = ["glazed", "powdered", "jelly"];`
  - `var mixedData = ["abcd", 1, true, undefined, null, "all the things"];` for `mixedData` array with mixed data types
  - `var arraysInArrays = [[1, 2, 3], ["Julia", "James"], [true, false, true, false]];` for nested array
- `donuts[11]` to access element of array
- Indexing starts at position zero
- `donuts[1] = "glazed cruller";` to change value of element in array

## Properties And Methods

- `myArray.length` returns number of elements in array
- `donuts.push("powdered")` adds element to end of array and returns length of array after element has been added
- `donuts.pop()` removes last element from end of array
- `donuts.splice(1, 1, "chocolate cruller", "creme de leche")` removes "chocolate frosted" at index 1 and adds "chocolate cruller" and "creme de leche" starting at index 1
- First argument represents starting index from where to change array, second argument represents numbers of elements to remove, remaining arguments represent elements to add

## Loops

- `donuts[0] += " hole"` addes " hole" to each string in donuts array

```
for (var i = 0; i < donuts.length; i++) {
    donuts[i] = donuts[i].toUpperCase();
```

- `myArray.forEach(myFunction)` to loop over array and apply "myFunction" to each element
- Could be defined as inline function expression, meaning whole function is entered within brackets of .forEach method

```
donuts.forEach(function(donut) {
  donut += " hole";
  donut = donut.toUpperCase();
  console.log(donut);
});
```

- `myArray.map(myFunction)` to loop over array and apply "myFunction" to each element and return new array

```
var improvedDonuts = donuts.map(function(donut) {
  donut += " hole";
  donut = donut.toUpperCase();
  return donut;
});
```

- For arrays in arrays

```
for (var row = 0; row < donutBox.length; row++) {
  // donutBox[row].length refers to length of donut array currently being looped over
  for (var column = 0; column < donutBox[row].length; column++) {
    console.log(donutBox[row][column]);
  }
}
```

# Objects

- Data structure that allows to store data about particular thing and helps to keep track of that data by using keys
- `var umbrella = {}` to create empty object
- `typeof umbrella` returns "object"
- Add properties and key value pairs

```
var umbrella = {
  color: "pink",
  isOpen: false,
  open: function() {
    if (umbrella.isOpen === true) {
      return "The umbrella is already opened!";
    } else {
      umbrella.isOpen = true;
      return "Julia opens the umbrella!";
    }
   }
};
```

- Following syntax is called object-literal notation
- Key representing property or method and its value are separated from each other by colon
- `key: value` pairs are separated from each other by commas
- Entire object is wrapped inside curly braces

```
var sister = {
  name: "Sarah",
  age: 23,
  parents: [ "alice", "andy" ],
  siblings: ["julia"],
  favoriteColor: "purple",
  pets: true,
  paintPicture: function() { return "Sarah paints!"; }
};
```

- Two equivalent ways to return values
- `sister["parents"]` called bracket notation returns [ "alice", "andy"]
- `sister.parents` called dot notation returns [ "alice", "andy" ]
- `sister.paintPicture();` to trigger respective function from object

```
var myObj = {
  color: "orange",
  shape: "sphere",
  type: "food",
  eat: function() { return "yummy" }
};

myObj.eat(); // method
myObj.color; // property
```

## Naming Conventions

- Do not use number as first character with quotes in property name
- Do not use spaces and hyphens

# Resources

- JavaScript Style Guide: [Google](https://google.github.io/styleguide/jsguide.html)
- Array documentation, properties and methods: [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)
- Splice documentation: [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/splice)
