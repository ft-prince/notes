JavaScript Cheat List
===

A JavaScript cheat sheet covering the most important concepts, functions, methods, and more. A complete quick reference for beginners.

getting Started
----

### introduce

JavaScript is a lightweight interpreted programming language.

- [JSON Cheat Sheet](json.md)
- [Regular Expressions in JavaScript](./regex.md#javascript-Regular Expressions)
- [TypeScript Cheat Sheet](./typescript.md)

### Print debugging

```javascript
// => Hello world!
console.log('Hello world!');
// => Hello QuickReference
console.warn('hello %s', 'QuickReference');
// Print error message to stderr
console.error(new Error('Oops!'));
```

### Breakpoint debugging

```javascript
function potentiallyBuggyCode() {
  debugger;
  // Do things that might be problematic to check, step through, etc.
}
```

The **debugger** statement invokes any available debugging functionality.

### number

```javascript
let amount = 6;
let price = 4.99;
let home = 1e2;
let num = 1_000_000; // If there are too many digits, you can use _ to divide them
let m = 0644; // octal number 420
```

### let keyword

```javascript
let count;
console.log(count); // => undefined
count = 10;
console.log(count); // => 10
```

### const keyword

```javascript
const numberOfColumns = 4;
// TypeError: Assignment to constant...
numberOfColumns = 8;
```

### Variables

```javascript
let x = null;
let name = "Tammy";
const found = false;
// => Tammy, false, null
console.log(name, found, x);
var a;
console.log(a); // => undefined
```

### string

```javascript
let single = 'Wheres my bandit hat?';
let double = "Wheres my bandit hat?";
// => 21
console.log(single.length);
```

### Arithmetic operators

```javascript
5 + 5 = 10 // Addition
10 - 5 = 5 // Subtraction
5 * 10 = 50 // MultiplicationMultiplication
10 / 5 = 2 // Division Division
10 % 5 = 0 // Modulo Modulo
```

### Comments

```javascript
// This line will represent a comment
/*
Multi-line configuration
Must be changed before deployment
The following configuration.
*/
```

### Assignment operator

```javascript
let number = 100;
// Both statements will add 10
number = number + 10;
number += 10;
console.log(number);
// => 120
```

### String interpolation

```javascript
let age = 7;
//String concatenation
'Tommy is ' + age + ' years old.';
// String interpolation
`Tommy is ${age} years old.`;
```

### string
<!--rehype:wrap-class=col-span-2-->

```js
var abc = "abcdefghijklmnopqrstuvwxyz";
var esc = 'I don\'t \n know'; // \n newline
var len = abc.length; // String length
abc.indexOf("lmno"); // Find substring, if not included then -1
abc.lastIndexOf("lmno"); // Last occurrence
abc.slice(3, 6); // Remove "def" and calculate negative values ​​from behind
abc.replace("abc","123"); // Find and replace, accept regular expressions
abc.toUpperCase(); // Convert to uppercase
abc.toLowerCase(); // Convert to lowercase
abc.concat(" ", str2); // abc + " " + str2
abc.charAt(2); //Character at index: "c"
abc[2]; // Unsafe, abc[2] = "C" does not work
//Character code at index: "c" -> 99
abc.charCodeAt(2);
// Split the string with commas to give an array
abc.split(",");
//split characters
abc.split("");
// Match the beginning string, if the second parameter is omitted, the match starts from index 0
abc.startsWith("bc", 1);
// Match the string at the end. If the second parameter is ignored, the default is the length of the original string.
abc.endsWith("wxy", abc.length - 1);
// padEnd and padStart are both used to fill the length. The default padding object is spaces.
"200".padEnd(5); // "200 "
"200".padEnd(5, "."); // "200.."
// Repeat characters
"abc".repeat(2); // "abcabc"
// trim, trimEnd and trimStart are used to remove leading and trailing spaces
" ab c ".trim(); // "ab c"
// Convert the number to hexadecimal (16), octal (8) or binary (2)
(128).toString(16);
```

### number
<!--rehype:wrap-class=row-span-2-->

```js
varpi = 3.141;
pi.toFixed(0); // return 3             
pi.toFixed(2); // returns 3.14 - use money
pi.toPrecision(2) // Return 3.1
pi.valueOf(); // return number
Number(true); // Convert to number
//Number of milliseconds since 1970
Number(new Date())          
// Return the first number: 3
parseInt("3 months");       
//return 3.5
parseFloat("3.5 days");     
// Maximum possible number of JS
Number.MAX_VALUE            
// Smallest possible JS number
Number.MIN_VALUE            
// - infinite
Number.NEGATIVE_INFINITY    
// infinite
Number.POSITIVE_INFINITY    
```

#### Math

```ts
const pi = Math.PI; // 3.141592653589793
Math.round(4.4); // = 4 - round the number
Math.round(4.5); // = 5
Math.pow(2,8); // = 256 - 2 raised to the 8th power    
Math.sqrt(49); // = 7 - square root
Math.abs(-3.14); // = 3.14 - absolute, positive value
Math.ceil(3.14); // = 4 - returns >= smallest integer
// = 3 - returns <= maximum integer
Math.floor(3.99);       
// = 0 - sine
Math.sin(0);            
// OTHERS: tan, atan, asin, acos, cosine value
Math.cos(Math.PI);      
// = -2 - lowest value
Math.min(0, 3, -2, 2);  
// = 3 - highest value
Math.max(0, 3, -2, 2);  
// = 0 natural logarithm
Math.log(1);            
// = 2.7182pow(E,x) base of natural logarithm
Math.exp(1);            
// Random number between 0 and 1
Math.random();          
// Random integer, starting from 1
Math.floor(Math.random() * 5) + 1;  
```

### Global function
<!--rehype:wrap-class=col-span-2-->

```js
//Execute string like script code
eval();                     
// Return string from number
String(23);                 
// Return string from number
(23).toString();            
// Return number from string
Number("23");               
// Decode URI. Result: "my page.asp"
decodeURI(enc);             
// Encode URI. Result: "my%20page.asp"
encodeURI(uri);             
//Decode URI component
decodeURIComponent(enc);    
// Encode the URI component
encodeURIComponent(uri);    
// is a limited legal number
isFinite();                 
// is an illegal number
isNaN();                    
//Return the floating point number of the string
parseFloat();               
// Parse a string and return an integer
parseInt();                 
```

JavaScript conditions
----

### Operator
<!--rehype:wrap-class=row-span-3-->

```javascript
true || false; // true
10 > 5 || 10 > 20; // true
false || false; // false
10 > 100 || 10 > 20; // false
```

#### Logical Operators&&

```javascript
true && true; // true
1 > 2 && 2 > 1; // false
true && false; // false
4 === 4 && 3 > 1; // true
```

#### Comparison operators

```javascript
1 > 3 // false
3 > 1 // true
250 >= 250 // true
1 === 1 // true
1 === 2 // false
1 === '1' // false
```

#### Logical Operators

```javascript
let lateToWork = true;
let oppositeValue = !lateToWork;
// => false
console.log(oppositeValue);
```

#### Null value coalescing operator??

```javascript
null ?? 'I win'; // 'I win'
undefined ?? 'Me too'; // 'Me too'
false ?? 'I lose' // false
0 ?? 'I lose again' // 0
'' ?? 'Damn it' // ''
```

### if Statement (if statement)

```javascript
const isMailSent = true;
if (isMailSent) {
  console.log('Mail sent to recipient');
}
```

### Ternary Operator (ternary operator)

```javascript
var age = 1;

// => true
var status = (age >= 18) ? true : false;
```

### else if

```javascript
const size = 10;
if (size > 20) {
  console.log('Medium');
} else if (size > 4) {
  console.log('Small');
} else {
  console.log('Tiny');
}
// Print: Small
```

### == vs ===

```javascript
0 == false // true
0 === false // false, different types
1 == "1" // true, automatic type conversion
1 === "1" // false, different types
null == undefined // true
null === undefined // false
'0' == false // true
'0' === false // false
```

`==` only checks the value, `===` checks both the value and the type.

### switch statement

```javascript
const food = 'salad';

switch (food) {
  case 'oyster': console.log('The smell of the sea');
    break;
  case 'pizza': console.log('delicious pie');
    break;
  default:
    console.log('Please have a meal');
}
```

### switch multicase - single operation

```javascript
const food = 'salad';

switch (food) {
  case 'oyster':
  case 'pizza':
    console.log('delicious pie');
    break;
  default:
    console.log('Please have a meal');
}
```

JavaScript Functions function
----

### Function

```javascript
//Define function:
function sum(num1, num2) {
  return num1 + num2;
}
// Call functions:
sum(3, 6); // 9
```

### Anonymous function

```javascript
// named function
function rocketToMars() {
  return 'BOOM!';
}
// Anonymous function
const rocketToMars = function() {
  return 'BOOM!';
}
```

### Arrow function (ES6)
<!--rehype:wrap-class=row-span-3-->

#### There are two parameters

```javascript
const sum = (param1, param2) => {
  return param1 + param2;
};
console.log(sum(2,5)); // => 7
```

#### No parameters

```javascript
const printHello = () => {
  console.log('hello');
};
printHello(); // => hello
```

#### Only one parameter

```javascript
const checkWeight = weight => {
  console.log(`Weight : ${weight}`);
};
checkWeight(25); // => Weight : 25
```

#### Concise arrow function

```javascript
const multiply = (a, b) => a * b;
// => 60
console.log(multiply(2, 30));
```

[Arrow functions] are provided starting from ES2015 (https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)

### Return keyword

```javascript
// There is return
function sum(num1, num2) {
  return num1 + num2;
}
// This function does not output the sum
function sum(num1, num2) {
  num1 + num2;
}
```

### Call functions

```javascript
//define function
function sum(num1, num2) {
  return num1 + num2;
}
// Call functions
sum(2, 4); // 6
```

### Execute function immediately

```javascript
//Name the function and execute it immediately
(function sum(num1, num2) {
  return num1 + num2;
})(2,4)//6
```

### Function expression

```javascript
const dog = function() {
  return 'Woof!';
}
```

### Function parameters

```javascript
//The parameter is name
function sayHello(name) {
  return `Hello, ${name}!`;
}
```

### Function declaration

```javascript
function add(num1, num2) {
  return num1 + num2;
}
```

JavaScript scope
----

### scope
<!--rehype:wrap-class=row-span-2-->

```javascript
function myFunction() {
  var pizzaName = "Margarita";
  // The code here can use PizzaName
  
}
// ❌ PizzaName cannot be used here
```

`{ }` variables declared within the block

```javascript
{
  let x = 2;
}
// ❌ x cannot be used here

{
  var x = 2;
}
// ✅ x can be used here
```

```javascript
var x = 2; // Global scope
let x = 2; // global scope
const x = 2; // Global scope
```

ES6 introduces two important new JavaScript keywords: let and const. These two keywords provide block scope in JavaScript.

### Block scope variables

```javascript
const isLoggedIn = true;
if (isLoggedIn == true) {
  const statusMessage = 'Logged in.';
}
// Uncaught ReferenceError...
// Uncaught reference error...
console.log(statusMessage);
```

### Global variables

```javascript
// Globally declared variables
const color = 'blue';
function printColor() {
  console.log(color);
}

printColor(); // => blue
```

### `let` vs `var`

```javascript
for (let i = 0; i < 3; i++) {
  // This is the maximum range of "let"
  // i can access ✔️
}
// i cannot access ❌
```

---

```javascript
for (var i = 0; i < 3; i++) {
  // i can access ✔️
}
// i can access ✔️
```

The scope of `var` is the nearest function block, and the scope of `let` is the nearest enclosing block.

### Loop with closure

```javascript
// Printing three times is not what we meant.
for (var i = 0; i < 3; i++) {
  setTimeout(_ => console.log(i), 10);
}
```

---

```javascript
// Prints 0, 1 and 2 as expected.
for (let j = 0; j < 3; j++) {
  setTimeout(_ => console.log(j), 10);
}
```

Variables have their own copy using `let`, variables have a shared copy using `var`.

JavaScript Arrays
----

### method
<!--rehype:wrap-class=row-span-6-->

:- | :-
:- | :-
`Array.from()` | Creates a new array object [#](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/from)
`Array.isArray()` | Whether the value is an Array [#](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/isArray)
`Array.of()` | Create a new array example[#](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/of)
`.at()` | Returns the element corresponding to the value index [#](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/at)
`.concat()` | Combine two or more arrays[#](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/concat)
`.copyWithin()` | Shallow copy replaces a certain position[#](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/copyWithin)
`.entries()` | New Array Iterator object[#](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/entries)
`.every()` | Whether it can pass the callback function test[#](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/every)
`.fill()` | Fill an array with a fixed value[#](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/fill)
`.filter()` | Returns the filtered array[#](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)
`.find()` | The value of the first element [#](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/find)
`.findIndex()` | Index of the first element [#](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/findIndex)
`.findLast()` | The value of the last element [#](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/findLast)
`.findLastIndex()` | Index of the last element [#](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/findLastIndex)
`.flat()` | Flatten nested arrays[#](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/flat)
`.flatMap()` | Same as flat[#](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/flatMap)
`.forEach()` | Ascending loop execution[#](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach)
`.includes()` | Whether to include a specified value[#](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/includes)
`.indexOf()` | Find the first index of the given element [#](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/indexOf)
`.join()` | Join an array into a string [#](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/join)
`.keys()` | Each index key [#](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/keys)
`.lastIndexOf()` | The last index of the given element [#](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/lastIndexOf)
`.map()` | Loop returns a new array[#](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/map)
`.pop()` | `Delete` the last element[#](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/pop)
`.push()` | Element `add` to the end of the array[#](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/push)
`.reduce()` | Loop function passes the current and previous values ​​[#](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce)
`.reduceRight()` | Similar to `reduce` looping from right to left[#](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/ReduceRight)
`.reverse()` | Reverse the position of array elements[#](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/reverse)
`.shift()` | `Delete` the first element[#](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/shift)
`.slice()` | `Extract` elements[#](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/slice)
`.some()` | At least one passing test function[#](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/some)
`.sort()` | Sort elements[#](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)
`.splice()` | `Remove` or `Replace` or `Add` element[#](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/splice )
`.toLocaleString()` | String represents the elements in the array[#](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/toLocaleString)
`.toString()` | Returns a string [#](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/toString)
`.unshift()` | Adds an element to the beginning of the array [#](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/unshift)
`.values()` | Returns a new ArrayIterator object[#](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/values)

### Array

```javascript
const fruits = ["apple", "dew", "banana"];
// different data types
const data = [1, 'chicken', false];
```

###property.length

```javascript
const numbers = [1, 2, 3, 4];
numbers.length // 4
```

### Index

```javascript
//Access array elements
const myArray = [100, 200, 300];
console.log(myArray[0]); // 100
console.log(myArray[1]); // 200
```

### Variable chart

| | Add | Delete | Start | End |
|:----------|:---:|:------:|:------:|:---:|
| `push` | ✅ | | | ✅ |
| `pop` | | ✅ | | ✅ |
| `unshift` | ✅ | | ✅ | |
| `shift` | | ✅ | ✅ | |
<!--rehype:className=show-header-->

### Method.push()

```javascript
// Add a single element:
const cart = ['apple', 'orange'];
cart.push('pear');
//Add multiple elements:
const numbers = [1, 2];
numbers.push(3, 4, 5);
```

Appends items to the end and returns the new array length.

### Method.pop()

```javascript
const fruits = ["apple", "dew", "banana"];
const fruit = fruits.pop(); // 'banana'

console.log(fruits); // ["apple", "dew"]
```

Removes an item from the end and returns the deleted item.

### Method.shift()

```javascript
const array1 = [1, 2, 3];
const firstElement = array1.shift();
console.log(array1); // Output: Array [2, 3]
console.log(firstElement); // Output: 1
```

**Delete** an item from the beginning and return the deleted item.

### Method.some()

```js
const array = [1, 2, 3, 4, 5];
// Check if the element is an even number
const even = (element) => element % 2 === 0;
console.log(array.some(even));
// expected output: true
```

### Method.concat()

```javascript
const numbers = [3, 2, 1]
const newFirstNumber = 4
    
// => [ 4, 3, 2, 1 ]
[newFirstNumber].concat(numbers)
    
// => [3, 2, 1, 4]
numbers.concat(newFirstNumber)
```

If you want to avoid changing your original array, you can use concat.

### Method.splice()

```javascript
const months = ['Jan', 'March'];
months.splice(1, 0, 'Feb');
//Insert at index 1
console.log(months);
// Expected output: Array ["Jan", "Feb", "March"]

months.splice(2, 1, 'May');
//Replace 1 element at index 2
console.log(months);
// Expected output: Array ["Jan", "Feb", "May"]
```

### Method.unshift()

```javascript
let cats = ['Bob'];
// => ['Willy', 'Bob']
cats.unshift('Willy');
// => ['Puff', 'George', 'Willy', 'Bob']
cats.unshift('Puff', 'George');
```

Adds an item to the beginning and returns the new array length.

### Method.filter()

```javascript
const words = ['js', 'java', 'golang'];
const result = words.filter(word => {
  return word.length > 3
});
console.log(result);
// Expected output: Array ["java", "golang"]
```

JavaScript loop
----

### While Loop

```javascript
while (condition) {
  //The code block to be executed
}
let i = 0;
while (i < 5) {        
  console.log(i);
  i++;
}
```

### Reverse loop

```javascript
const fruits = ["apple", "dew", "berry"];
for (let i = fruits.length - 1; i >= 0; i--) {
  console.log(`${i}. ${fruits[i]}`);
}
// => 2. berry
// => 1. dew
// => 0. apple
```

### Do...While statement

```javascript
x = 0
i = 0
do {
  x = x + i;
  console.log(x)
  i++;
} while (i < 5);
// => 0 1 3 6 10
```

### For loop

```javascript
for (let i = 0; i < 4; i += 1) {
  console.log(i);
};
// => 0, 1, 2, 3
```

### Traverse the array

```javascript
for (let i = 0; i < array.length; i++){
  console.log(array[i]);
}
// => each item in the array
```

### Break

```javascript
for (let i = 0; i < 99; i += 1) {
  if (i > 5) break;
  console.log(i)
}
// => 0 1 2 3 4 5
```

### Continue

```javascript
for (i = 0; i < 10; i++) {
  if (i === 3) {
    continue;
  }
  text += "The number is " + i + "<br>";
}
```

### Nested loops

```javascript
for (let i = 0; i < 2; i += 1) {
  for (let j = 0; j < 3; j += 1) {
    console.log(`${i}-${j}`);
  }
}
```

### for...in loop

```javascript
const fruits = ["apple", "orange", "banana"];
for (let index in fruits) {
  console.log(index);
}
// => 0
// => 1
// => 2
```

### label statement
<!--rehype:wrap-class= row-span-2-->

```js
varnum = 0;

outPoint:
for(var i = 0; i < 10; i++) {
  for(var j = 0; j < 10; j++) {
    if(i == 5 && j == 5) {
      continue outPoint;
    }
    num++;
  }
}

alert(num); // 95
```

It can be seen from the value of `alert(num)` that the function of `continue outPoint;` statement is to jump out of the current loop and jump to the `for` loop under `outPoint` (label) to continue execution.

### for...of loop

```javascript
const fruits = ["apple", "orange", "banana"];
for (let fruit of fruits) {
  console.log(fruit);
}
// => apple
// => orange
// => banana
```

### for await...of
<!--rehype:wrap-class= row-span-2-->

```javascript
async function* asyncGenerator() {
  var i = 0;
  while (i < 3) {
    yield i++;
  }
}

(async function() {
  for await (num of asyncGenerator()) {
    console.log(num);
  }
})();

// 0
// 1
// 2
```

### Optional for expression

```js
var i = 0;

for (;;) {
  if (i > 3) break;
  console.log(i);
  i++;
}
```

JavaScript Iterators
----
<!--rehype:body-class=cols-2-->

### Function assigned to variable

```javascript
let plusFive = (number) => {
  return number + 5;  
};
// f is assigned plusFive
let f = plusFive;
plusFive(3); // 8
// Since f has a function value, it can be called.
f(9); // 14
```

### Callback

```javascript
const isEven = (n) => {
  return n % 2 == 0;
}
let printMsg = (evenFunc, num) => {
  const isNumEven = evenFunc(num);
  console.log(`${num} is an even number: ${isNumEven}.`)
}
// Pass in isEven as the callback function
printMsg(isEven, 4);
// => The number 4 is an even number: True.
```

### Array method.reduce()

```javascript
const numbers = [1, 2, 3, 4];
const sum = numbers.reduce((accumulator, curVal) => {  
  return accumulator + curVal;
});
console.log(sum); // 10
```

### Array method.map()

```javascript
const members = ["Taylor", "Donald", "Don", "Natasha", "Bobby"];
const announcements = members.map((member) => {
  return member + "joined the contest.";
});
console.log(announcements);
```

### Array method.forEach()

```javascript
const numbers = [28, 77, 45, 99, 27];
numbers.forEach(number => {  
  console.log(number);
});
```

### Array method.filter()

```javascript
const randomNumbers = [4, 11, 42, 14, 39];
const filteredArray = randomNumbers.filter(n => {  
  return n > 5;
});
```

JavaScript Objects
----
<!--rehype:body-class=cols-2-->

### Access properties

```javascript
const apple = {
  color: 'Green',
  price: { bulk: '$3/kg', smallQty: '$4/kg' }
};
console.log(apple.color); // => Green
console.log(apple.price.bulk); // => $3/kg
```

### Named properties

```javascript
//Invalid key name example
const trainSchedule = {
  // Invalid due to spaces between words.
  platform num: 10,
  //Expression cannot be a key.
  40 - 10 + 2: 30,
  // The + sign has no effect unless enclosed in quotes.
  +compartment: 'C'
}
```

### Non-existent attribute

```javascript
const classElection = {
  date: 'January 12'
};
console.log(classElection.place); // undefined
```

### Variable
<!--rehype:wrap-class=row-span-2-->

```javascript
const student = {
  name: 'Sheldon',
  score: 100,
  grade: 'A',
}
console.log(student)
// { name: 'Sheldon', score: 100, grade: 'A' }
delete student.score
student.grade = 'F'
console.log(student)
// { name: 'Sheldon', grade: 'F' }
student = {}
// TypeError: TypeError: assigned to constant variable.
```

### Assignment shorthand syntax

```javascript
const person = {
  name: 'Tom',
  age: '22',
};
const {name, age} = person;
console.log(name); // 'Tom'
console.log(age); // '22'
```

### Delete operator

```javascript
const person = {
  firstName: "Matilda",
  hobby: "knitting",
  goal: "learning JavaScript"
};
delete person.hobby; // or delete person['hobby'];
console.log(person);
/*
{
  firstName: "Matilda"
  goal: "learning JavaScript"
} */
```

### Object as parameter

```javascript
const origNum = 8;
const origObj = {color: 'blue'};
const changeItUp = (num, obj) => {
  num = 7;
  obj.color = 'red';
};
changeItUp(origNum, origObj);
// will output 8 because integers are passed by value.
console.log(origNum);
// Since the object was passed, "red" will be output
// By reference, therefore mutable.
console.log(origObj.color);
```

### Factory function
<!--rehype:wrap-class=row-span-2-->

```javascript
// A factory function that accepts 'name', 'age' and 'breed',
//The parameter returns a custom dog object.
const dogFactory = (name, age, breed) => {
  return {
    name: name,
    age: age,
    breed: breed,
    bark() {
      console.log('Woof!');  
    }
  };
};
```

### Shorthand object creation

```javascript
const activity = 'Surfing';
const beach = { activity };
console.log(beach); // { activity: 'Surfing' }
```

### this keyword

```javascript
const cat = {
  name: 'Pipey',
  age: 8,
  whatName() {
    return this.name  
  }
};
console.log(cat.whatName()); // => Pipey
```

### method

```javascript
const engine = {
  //Method abbreviation, with one parameter
  start(adverb) {
    console.log(`The engine starts up ${adverb}...`);
  },  
  // Anonymous arrow function expression without parameters
  sputter: () => {
    console.log('The engine sputters...');
  },
};
engine.start('noisily');
engine.sputter();
```

### Getters and setters

```javascript
const myCat = {
  _name: 'Dottie',
  get name() {
    return this._name;  
  },
  set name(newName) {
    this._name = newName;  
  }
};
//Reference call getter
console.log(myCat.name);
// Assignment calls setter
myCat.name = 'Yankee';
```

### Proxy

The Proxy object is used to create a proxy for an object to implement interception and customization of basic operations (such as property lookup, assignment, enumeration, function calling, etc.).

```javascript
// Used to intercept the read property operation of the object.
const handler = {
    get: function(obj, prop) {
        return prop in obj ? obj[prop] : 37;
    }
};

const p = new Proxy({}, handler);
pa = 1;
pb = undefined;

console.log(pa, pb); // 1, undefined
console.log('c' in p, pc); // false, 37
```

#### grammar

```javascript
const p = new Proxy(target, handler)
```

- target The target object to be wrapped using the Proxy (can be any type of object, including a native array, a function, or even another proxy).
- handler is an object that usually has functions as attributes. The functions in each attribute define the behavior of agent p when performing various operations.

#### method

:- | :-
:- | :-
`Proxy.revocable()` | Create a revocable Proxy object[#](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Proxy/revocable)

#### Methods of handler objects

:- | :-
:- | :-
`handler.getPrototypeOf()` | Catcher for the Object.getPrototypeOf method[#](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Proxy/Proxy/getPrototypeOf)
`handler.setPrototypeOf()` | Catcher for the Object.setPrototypeOf method[#](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Proxy/Proxy/setPrototypeOf)
`handler.isExtensible()` | Object.isExtensible method catcher[#](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Proxy/Proxy/isExtensible)
`handler.preventExtensions()` | Object.preventExtensions method catcher[#](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Proxy/Proxy/preventExtensions)
`handler.getOwnPropertyDescriptor()` | Object.getOwnPropertyDescriptor method catcher[#](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Proxy/Proxy/getOwnPropertyDescriptor)
`handler.defineProperty()` | Object.defineProperty method catcher[#](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Proxy/Proxy/defineProperty)
`handler.has()` | in operator catcher[#](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Proxy/Proxy/has)
`handler.get()` | Catcher for property reading operations[#](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Proxy/Proxy/get)
`handler.set()` | Catcher for property setting operations[#](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Proxy/Proxy/set)
`handler.deleteProperty()` | Catcher of delete operator[#](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Proxy/Proxy/deleteProperty)
`handler.ownKeys()` | Catchers for the Object.getOwnPropertyNames method and the Object.getOwnPropertySymbols method [#](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Proxy/ Proxy/ownKeys)
`handler.apply()` | Function call operation catcher[#](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Proxy/Proxy/apply)
`handler.construct()` | new operator’s catcher[#](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Proxy/Proxy/construct)
<!--rehype:className=style-list-arrow-->

### Reflect

Reflect is a built-in object that provides methods for intercepting JavaScript operations. These methods are identical to those of proxy handlers (en-US). Reflect is not a function object, so it is not constructible.

```javascript
//Detect whether an object has a specific attribute
const duck = {
  name: 'Maurice',
  color: 'white',
  greeting: function() {
    console.log(`Quaaaack! My name is ${this.name}`);
  }
}

Reflect.has(duck, 'color');
// true
Reflect.has(duck, 'haircut');
// false
```

#### Static method

:- | :-
:- | :-
`Reflect.apply(target, thisArgument, argumentsList)` | Call a function and pass in an array as the calling parameter. Similar to Function.prototype.apply()[#](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Reflect/apply)
`Reflect.construct(target, argumentsList[, newTarget])` | Performing a new operation on the constructor is equivalent to executing new target(...args) [#](https://developer.mozilla.org/zh-CN /docs/Web/JavaScript/Reference/Global_Objects/Reflect/construct)
`Reflect.defineProperty(target, propertyKey, attributes)` | Similar to Object.defineProperty(). If the setting is successful, it will return true [#](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Reflect/defineProperty)
`Reflect.deleteProperty(target, propertyKey)` | As the delete operator of a function, it is equivalent to executing delete target[name] [#](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/ Reference/Global_Objects/Reflect/deleteProperty)
`Reflect.get(target, propertyKey[, receiver])` | Get the value of a property on the object, similar to target[name] [#](https://developer.mozilla.org/zh-CN/docs/ Web/JavaScript/Reference/Global_Objects/Reflect/get)
`Reflect.getOwnPropertyDescriptor(target, propertyKey)` | Similar to Object.getOwnPropertyDescriptor(). If the property exists in the object, the corresponding property descriptor is returned, otherwise undefined [#](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Reflect/getOwnPropertyDescriptor)
`Reflect.getPrototypeOf(target)` | Similar to Object.getPrototypeOf() [#](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Reflect/getPrototypeOf)
`Reflect.has(target, propertyKey)` | Determine whether an object has a certain property, which has the same function as the in operator[#](https://developer.mozilla.org/zh-CN/docs/Web/ JavaScript/Reference/Global_Objects/Reflect/has)
`Reflect.isExtensible(target)` | Similar to Object.isExtensible() [#](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Reflect/isExtensible)
`Reflect.ownKeys(target)` | Returns an array containing all own properties (excluding inherited properties). (Similar to Object.keys(), but will not be affected by enumerable) [#](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Reflect/ownKeys)
`Reflect.preventExtensions(target)` | Similar to Object.preventExtensions(). Returns a Boolean [#](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Reflect/preventExtensions)
`Reflect.set(target, propertyKey, value[, receiver])` | Function that assigns a value to a property. Returns a Boolean, or true if the update is successful [#](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Reflect/set)
`Reflect.setPrototypeOf(target, prototype)` | Function to set the prototype of an object. Returns a Boolean, or true if the update is successful [#](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Reflect/setPrototypeOf)
<!--rehype:className=style-list-arrow-->

JavaScript this binding
----

### Implicit binding

```js
function foo() {
  console.log(this)
}
let obj1 = {
  name: "obj1",
  foo: foo
}
let obj2 = {
  name: "obj2",
  obj1: obj1
}
obj2.obj1.foo() // [Object obj1]
```

#### Implicit loss

```js
let a = obj2.obj1.foo()
a() // Window
```

- Specify implicit binding: there must be a reference to the function (such as a property) inside the calling object
- Assign the above call to a variable, and the result will eventually be Window
- No explicit binding is done where a is called, and eventually the global object window will call it (`Window.a`)
<!--rehype:className=style-round-->

### Show binding

```js
function getName(a1, a2) {
  console.log("this person" + this.name, "age" + (a1 + a2))
}
let person = {
  name: "zhangsan"
}
```

#### call

The first parameter of call accepts the this scope, and the remaining parameters are passed to the function it calls.

```js
getName.call(person, 18, 12)
```

#### apply

The first parameter of apply is the same as call, and the second parameter is the parameter array of the calling function.

```js
getName.apply(person, [18, 12])
```

#### bind

The bind function returns a new function

```js
getName.bind(person,18,12)()
//Or it can be like this
getName.bind(person)(18, 12)
//Or this
getName.bind(person).bind(null, 18)(12)
```

### this in built-in functions

Some methods in the array, similar to map, forEach, etc., you can set the binding this yourself

```js
const obj = {
  name: "zhangsan"
}
const array = [1, 2, 3];
array.map(function(value){
  console.log(this.name)
}, obj)
// zhangsan x3
```

Some of the global objects, such as setTimeout, etc., like some array methods that do not explicitly bind this, will point to the global object (`Window`)

```js
setTimeout(function(){
  console.log(this)
}, 1000) // Window
```

JavaScript Classes
----

### Static methods/fields
<!--rehype:wrap-class=row-span-2-->

```javascript
class Dog {
  constructor(name) {
    this._name = name;  
  }
  
  introduce() {
    console.log('This is ' + this._name + ' !');  
  }
  
  // static method
  static bark() {
    console.log('Woof!');  
  }

  static {
    console.log('Class static initialization block call');
  }
}

const myDog = new Dog('Buster');
myDog.introduce();

// Call static method
Dog.bark();
```

#### Public static fields

```js
class ClassStaticField {
  static staticField = 'static field'
}

console.log(ClassStaticField.staticField)
// Expected output value: "static field"​
```

### Class

```javascript
class Song {
  constructor() {
    this.title;
    this.author;
  }
  
  play() {
    console.log('Song playing!');
  }
}

const mySong = new Song();
mySong.play();
```

### extends

```javascript
// Parent class
class Media {
  constructor(info) {
    this.publishDate = info.publishDate;
    this.name = info.name;
  }
}
// Child class
class Song extends Media {
  constructor(songData) {
    super(songData);
    this.artist = songData.artist;
  }
}
const mySong = new Song({
  artist: 'Queen',
  name: 'Bohemian Rhapsody',
  publishDate: 1975
});
```

### Class Constructor

```javascript
class Song {
  constructor(title, artist) {
    this.title = title;
    this.artist = artist;
  }
}
const mySong = new Song('Bohemian Rhapsody', 'Queen');
console.log(mySong.title);
```

### Class Methods

```javascript
class Song {
  play() {
    console.log('Playing!');
  }
  
  stop() {
    console.log('Stopping!');
  }
}
```

JavaScript Modules
----
<!--rehype:body-class=cols-2-->

### Export/Import

```javascript
// myMath.js
//Default exportDefault export
export default function add(x,y){
  return x + y
}
//Normal exportNormal export
export function subtract(x,y){
  return x-y
}
//Multiple exportsMultiple exports
function multiply(x,y){
  return x*y
}
function duplicate(x){
  return x * 2
}
export {
  multiply, duplicate
}
```

#### import load module

```javascript
// main.js
import add, { subtract, multiply, duplicate } from './myMath.js';
console.log(add(6, 2)); // 8
console.log(subtract(6, 2)) // 4
console.log(multiply(6, 2)); // 12
console.log(duplicate(5)) // 10
// index.html
<script type="module" src="main.js"></script>
```

### Export Module

```javascript
// myMath.js
function add(x,y){
  return x + y
}
function subtract(x,y){
  return x-y
}
function multiply(x,y){
  return x*y
}
function duplicate(x){
  return x * 2
}
// Multiple exports in node.js
module.exports = {
  add,
  subtract,
  multiply,
  duplicate
}
```

#### require load module

```javascript
// main.js
const myMath = require('./myMath.js')
console.log(myMath.add(6, 2)); // 8
console.log(myMath.subtract(6, 2)) // 4
console.log(myMath.multiply(6, 2)); // 12
console.log(myMath.duplicate(5)) // 10
```

JavaScript Promises
----

### Promise
<!--rehype:wrap-class=row-span-2-->

Create promises

```javascript
new Promise((resolve, reject) => {
  if (ok) {
    resolve(result)
  } else {
    reject(error)
  }
})
```

#### Using promises

```javascript
promise
  .then((result) => { ··· })
  .catch((error) => { ··· })
```

#### Promise method

```javascript
Promise.all(···)
Promise.race(···)
Promise.reject(···)
Promise.resolve(···)
```

### Executor function

```javascript
const executorFn = (resolve, reject) => {
  resolve('Resolved!');
};
const promise = new Promise(executorFn);
```

### setTimeout()

```javascript
const loginAlert = () => {
  console.log('Login');
};
setTimeout(loginAlert, 6000);
```

### Promise status

```javascript
const promise = new Promise((resolve, reject) => {
  const res = true;
  // An asynchronous operation.
  if (res) {
    resolve('Resolved!');
  }
  else {
    reject(Error('Error'));
  }
});
promise.then(
  (res) => console.log(res),
  (err) => console.error(err)
);
```

### .then() method

```javascript
const promise = new Promise((resolve, reject) => {    
  setTimeout(() => {
    resolve('Result');
  }, 200);
});

promise.then((res) => {
  console.log(res);
}, (err) => {
  console.error(err);
});
```

### .catch() method

```javascript
const promise = new Promise(
  (resolve, reject) => {  
  setTimeout(() => {
    reject(Error('Promise is unconditionally rejected.'));
  }, 1000);
});

promise.then((res) => {
  console.log(value);
});

promise.catch((err) => {
  console.error(err);
});
```

### Promise.all()
<!--rehype:wrap-class=col-span-2-->

```javascript
const promise1 = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve(3);
  }, 300);
});
const promise2 = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve(2);
  }, 200);
});
Promise.all([promise1, promise2]).then((res) => {
  console.log(res[0]);
  console.log(res[1]);
});
```

### Chain multiple .then()

```javascript
const promise = new Promise(
  resolve =>
    setTimeout(() => resolve('dAlan'),100)
);

promise.then(res => {
  return res === 'Alan'
    ? Promise.resolve('Hey Alan!')
    : Promise.reject('Who are you?')
})
.then((res) => {
  console.log(res)
}, (err) => {
  console.error(err)
});
```

### Avoid nested Promise and .then()
<!--rehype:wrap-class=col-span-2-->

```javascript
const promise = new Promise((resolve, reject) => {  
  setTimeout(() => {
    resolve('*');
  }, 1000);
});
const twoStars = (star) => {  
  return (star + star);
};
const oneDot = (star) => {  
  return (star + '.');
};
const print = (val) => {
  console.log(val);
};
// link them together
promise.then(twoStars).then(oneDot).then(print);
```

JavaScript Async-Await
----
<!--rehype:body-class=cols-2-->

### Asynchronous
<!--rehype:wrap-class=row-span-2-->

```javascript
function helloWorld() {
  return new Promise(resolve => {
    setTimeout(() => {
      resolve('Hello World!');
    }, 2000);
  });
}

// Asynchronous function expression
const msg = async function() {
  const msg = await helloWorld();
  console.log('Message:', msg);
}

// Asynchronous arrow function
const msg1 = async () => {
  const msg = await helloWorld();
  console.log('Message:', msg);
}

msg(); // Message: Hello World! <-- 2 seconds later
msg1(); // Message: Hello World! <-- 2 seconds later
```

### Resolve Promises

```javascript
let pro1 = Promise.resolve(5);
let pro2 = 44;
let pro3 = new Promise(function(resolve, reject) {
  setTimeout(resolve, 100, 'foo');
});
Promise.all([pro1, pro2, pro3]).then(function(values) {
  console.log(values);
});
// expected => Array [5, 44, "foo"]
```

### Asynchronously wait for Promises

```javascript
function helloWorld() {
  return new Promise(resolve => {
    setTimeout(() => {
      resolve('Hello World!');
    }, 2000);
  });
}
async function msg() {
  const msg = await helloWorld();
  console.log('Message:', msg);
}
msg(); // Message: Hello World! <-- 2 seconds later
```

### Error handling

```javascript
// incomplete data
let json = '{ "age": 30 }';

try {
  let user = JSON.parse(json); // <-- no error
  console.log( user.name ); // no name!
} catch (e) {
  console.error( "Invalid JSON data!" );
}
```

### Asynchronous await operator

```javascript
function helloWorld() {
  return new Promise(resolve => {
    setTimeout(() => {
      resolve('Hello World!');
    }, 2000);
  });
}
async function msg() {
  const msg = await helloWorld();
  console.log('Message:', msg);
}
msg(); // Message: Hello World! <-- 2 seconds later
```

JavaScript request
----

### JSON

```JS
const jsonObj = {
  "name": "Rick",
  "id": "11A",
  "level": 4  
};
```

See also: [JSON Cheat Sheet](./json.md)

### XMLHttpRequest

```javascript
const xhr = new XMLHttpRequest();
xhr.open('GET', 'mysite.com/getjson');
```

`XMLHttpRequest` is a browser-level API that enables clients to script data transfer via JavaScript, rather than being part of the JavaScript language.

###GET

```javascript
const req = new XMLHttpRequest();
req.responseType = 'json';
req.open('GET', '/getdata?id=65');
req.onload = () => {
  console.log(xhr.response);
};
req.send();
```

### POST
<!--rehype:wrap-class=row-span-2-->

```javascript
const data = { weight: '1.5 KG' };
const xhr = new XMLHttpRequest();
//Initialize a request.
xhr.open('POST', '/inventory/add');
// An enumeration value used to define the response type
xhr.responseType = 'json';
//Send request and data.
xhr.send(JSON.stringify(data));
// Fired when the request completes successfully.
xhr.onload = () => {
  console.log(xhr.response);
}
// Fired when request encounters an error.
xhr.onerror = () => {
  console.log(xhr.response);
}
```

### fetch api
<!--rehype:wrap-class=row-span-2-->

```javascript
fetch(url, {
    method: 'POST',
    headers: {
      'Content-type': 'application/json',
      'apikey': apiKey
    },
    body:data
}).then(response => {
  if (response.ok) {
    return response.json();
  }
  throw new Error('Request failed!');
}, networkError => {
  console.log(networkError.message)
})
```

### JSON format

```javascript
fetch('url-that-returns-JSON')
  .then(response => response.json())
  .then(jsonResponse => {
    console.log(jsonResponse);
  });
```

### promise url parameter acquisition API

```javascript
fetch('url')
  .then(response => {
    console.log(response);
  }, rejection => {
    console.error(rejection.message);
  });
```

### Fetch API function

```javascript
fetch('https://api-xxx.com/endpoint', {
  method: 'POST',
  body: JSON.stringify({id: "200"})
}).then(response => {
  if(response.ok){
    return response.json();  
  }
  throw new Error('Request failed!');
}, networkError => {
  console.log(networkError.message);
}).then(jsonResponse => {
  console.log(jsonResponse);
})
```

### async await syntax
<!--rehype:wrap-class=col-span-2-->

```javascript
const getSuggestions = async () => {
  const wordQuery = inputField.value;
  const endpoint = `${url}${queryParams}${wordQuery}`;
  try{
    const response = await fetch(endpoint, {cache: 'no-cache'});
    if(response.ok){
      const jsonResponse = await response.json()
    }
  }
  catch(error){
    console.log(error)
  }
}
```
