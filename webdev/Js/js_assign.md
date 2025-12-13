# JavaScript Mastery Curriculum

> A comprehensive progression from beginner to expert level with 280+ assignments

---

# 🟢 BEGINNER LEVEL

## Module 1: Variables and Data Types

### Assignment B1: Variable Declaration Basics
**Difficulty:** ⭐ (1/5) | **Time:** 15 mins

**Problem Statement:**
Create a program that declares variables using `var`, `let`, and `const` to store personal information.

**Requirements:**
1. Declare a `const` for your birth year
2. Declare a `let` for your current age
3. Declare a `var` for your name
4. Attempt to reassign the `const` and observe the error
5. Log all values to console

**Expected Output:**
```
Name: John
Age: 25
Birth Year: 1998
```

**Test Cases:**
- Variables should hold correct types
- `const` reassignment should throw TypeError
- `let` should be reassignable

**Learning Objectives:**
- Understand difference between var, let, const
- Know when to use each declaration type
- Understand immutability of const

**Hints:**
- const doesn't make objects immutable, only the binding
- Use descriptive variable names

**Common Mistakes:**
- Using var in modern code
- Trying to reassign const
- Not initializing const at declaration

**Extension:** Create an object with const and modify its properties.

---

### Assignment B2: Data Type Explorer
**Difficulty:** ⭐ (1/5) | **Time:** 20 mins

**Problem Statement:**
Create variables of each primitive data type and log their types.

**Requirements:**
1. Create one variable for each: string, number, boolean, undefined, null, symbol, bigint
2. Use `typeof` operator on each
3. Note the quirk with `typeof null`

**Expected Output:**
```
string: "string"
number: "number"
boolean: "boolean"
undefined: "undefined"
null: "object" (JavaScript quirk!)
symbol: "symbol"
bigint: "bigint"
```

**Test Cases:**
```javascript
typeof "hello" === "string"
typeof 42 === "number"
typeof true === "boolean"
typeof undefined === "undefined"
typeof null === "object" // Known quirk
typeof Symbol() === "symbol"
typeof 9007199254740991n === "bigint"
```

**Learning Objectives:**
- Identify all JavaScript primitive types
- Use typeof operator correctly
- Understand the null typeof quirk

**Hints:**
- BigInt is created with `n` suffix or BigInt()
- Symbol creates unique identifiers

**Common Mistakes:**
- Forgetting null returns "object"
- Confusing undefined and null

**Extension:** Use `Object.prototype.toString.call()` for accurate type checking.

---

### Assignment B3: Type Coercion Detective
**Difficulty:** ⭐⭐ (2/5) | **Time:** 25 mins

**Problem Statement:**
Predict and verify the results of various type coercion operations.

**Requirements:**
Evaluate and explain each expression:
```javascript
"5" + 3
"5" - 3
"5" * "2"
true + true
false + null
"hello" - 1
[] + []
[] + {}
{} + []
```

**Expected Output:**
```
"5" + 3 = "53" (string concatenation)
"5" - 3 = 2 (numeric subtraction)
"5" * "2" = 10 (numeric multiplication)
true + true = 2 (boolean to number)
false + null = 0 (both coerce to 0)
"hello" - 1 = NaN (invalid number)
[] + [] = "" (empty string)
[] + {} = "[object Object]"
{} + [] = 0 (block statement + array)
```

**Learning Objectives:**
- Understand implicit type coercion
- Know when + concatenates vs adds
- Predict coercion behavior

**Hints:**
- + with strings triggers concatenation
- Other operators trigger numeric coercion

**Common Mistakes:**
- Assuming + always adds
- Not understanding NaN results

**Extension:** Create a function that safely adds two values of any type.

---

### Assignment B4: Explicit Type Conversion
**Difficulty:** ⭐⭐ (2/5) | **Time:** 20 mins

**Problem Statement:**
Write functions to explicitly convert between types.

**Requirements:**
```javascript
function toNumber(value) { /* convert to number */ }
function toString(value) { /* convert to string */ }
function toBoolean(value) { /* convert to boolean */ }
```

**Test Cases:**
```javascript
toNumber("42") === 42
toNumber("hello") // NaN
toNumber(true) === 1
toString(123) === "123"
toString(null) === "null"
toBoolean(0) === false
toBoolean("hello") === true
toBoolean("") === false
```

**Learning Objectives:**
- Use Number(), String(), Boolean() constructors
- Understand falsy values
- Handle edge cases in conversion

**Hints:**
- Falsy values: 0, "", null, undefined, NaN, false
- parseInt/parseFloat for string parsing

**Common Mistakes:**
- Forgetting NaN is a number type
- Not handling null/undefined

**Extension:** Create a function that detects if conversion will produce NaN.

---

### Assignment B5: Arithmetic Operators
**Difficulty:** ⭐ (1/5) | **Time:** 20 mins

**Problem Statement:**
Create a basic calculator that performs all arithmetic operations.

**Requirements:**
```javascript
function calculate(a, b, operator) {
  // Return result of operation
  // Operators: +, -, *, /, %, **
}
```

**Test Cases:**
```javascript
calculate(10, 3, '+') === 13
calculate(10, 3, '-') === 7
calculate(10, 3, '*') === 30
calculate(10, 3, '/') === 3.333...
calculate(10, 3, '%') === 1
calculate(2, 3, '**') === 8
calculate(10, 0, '/') === Infinity
```

**Learning Objectives:**
- Master all arithmetic operators
- Handle division by zero
- Understand modulo and exponentiation

**Hints:**
- ** is the exponentiation operator
- Division by zero returns Infinity

**Common Mistakes:**
- Not handling division by zero
- Confusing % with division

**Extension:** Add support for unary operators (++, --).

---

### Assignment B6: Comparison Operators
**Difficulty:** ⭐⭐ (2/5) | **Time:** 25 mins

**Problem Statement:**
Create a comparison utility that demonstrates all comparison operators.

**Requirements:**
Implement and test:
```javascript
function compare(a, b) {
  return {
    equal: a == b,
    strictEqual: a === b,
    notEqual: a != b,
    strictNotEqual: a !== b,
    lessThan: a < b,
    greaterThan: a > b,
    lessOrEqual: a <= b,
    greaterOrEqual: a >= b
  };
}
```

**Test Cases:**
```javascript
compare(5, "5")
// equal: true, strictEqual: false
compare(null, undefined)
// equal: true, strictEqual: false
compare(NaN, NaN)
// equal: false, strictEqual: false
compare([], [])
// equal: false (different references)
```

**Learning Objectives:**
- Difference between == and ===
- Reference vs value comparison
- Special cases (NaN, null, undefined)

**Hints:**
- Always prefer === over ==
- NaN is never equal to anything, including itself

**Common Mistakes:**
- Using == instead of ===
- Expecting NaN === NaN to be true

**Extension:** Create an isEqual function for deep object comparison.

---

### Assignment B7: Logical Operators
**Difficulty:** ⭐⭐ (2/5) | **Time:** 20 mins

**Problem Statement:**
Create a permission checker using logical operators.

**Requirements:**
```javascript
function checkAccess(user) {
  // user: { isLoggedIn, isAdmin, isPremium, age }
  // Return access level based on conditions:
  // "full" - admin OR (premium AND logged in)
  // "limited" - logged in AND age >= 18
  // "none" - otherwise
}
```

**Test Cases:**
```javascript
checkAccess({isAdmin: true}) === "full"
checkAccess({isLoggedIn: true, isPremium: true}) === "full"
checkAccess({isLoggedIn: true, age: 25}) === "limited"
checkAccess({isLoggedIn: false}) === "none"
```

**Learning Objectives:**
- Use &&, ||, ! operators
- Understand short-circuit evaluation
- Combine logical conditions

**Hints:**
- && returns first falsy or last value
- || returns first truthy or last value

**Common Mistakes:**
- Not considering short-circuit evaluation
- Incorrect operator precedence

**Extension:** Add the nullish coalescing operator (??) for default values.

---

### Assignment B8: Assignment Operators
**Difficulty:** ⭐ (1/5) | **Time:** 15 mins

**Problem Statement:**
Create a score tracker using all assignment operators.

**Requirements:**
```javascript
let score = 0;
// Use +=, -=, *=, /=, %=, **= operators
// Track operations history
```

**Expected Output:**
```
Initial: 0
After += 10: 10
After *= 2: 20
After -= 5: 15
After /= 3: 5
After **= 2: 25
After %= 7: 4
```

**Learning Objectives:**
- Master compound assignment operators
- Understand operation order
- Track state changes

**Extension:** Add logical assignment operators (&&=, ||=, ??=).

---

### Assignment B9: Ternary Operator
**Difficulty:** ⭐⭐ (2/5) | **Time:** 20 mins

**Problem Statement:**
Refactor if/else statements to ternary operators.

**Requirements:**
```javascript
// Convert to ternary:
function getGrade(score) {
  if (score >= 90) return 'A';
  else if (score >= 80) return 'B';
  else if (score >= 70) return 'C';
  else if (score >= 60) return 'D';
  else return 'F';
}
```

**Test Cases:**
```javascript
getGrade(95) === 'A'
getGrade(85) === 'B'
getGrade(75) === 'C'
getGrade(65) === 'D'
getGrade(55) === 'F'
```

**Learning Objectives:**
- Use nested ternary operators
- Know when ternary is appropriate
- Improve code conciseness

**Hints:**
- Nested ternaries can reduce readability
- Format with proper indentation

**Common Mistakes:**
- Over-nesting ternaries
- Forgetting the else case

**Extension:** Rewrite using an object lookup for better readability.

---

### Assignment B10: Template Literals
**Difficulty:** ⭐ (1/5) | **Time:** 15 mins

**Problem Statement:**
Create a profile card generator using template literals.

**Requirements:**
```javascript
function createProfileCard(user) {
  // user: { name, age, city, hobbies: [] }
  // Return formatted multi-line string
}
```

**Expected Output:**
```
╔══════════════════════╗
║ Profile Card         ║
╠══════════════════════╣
║ Name: John Doe       ║
║ Age: 25              ║
║ City: New York       ║
║ Hobbies:             ║
║   - Reading          ║
║   - Coding           ║
╚══════════════════════╝
```

**Learning Objectives:**
- Use template literal syntax
- Embed expressions in strings
- Create multi-line strings

**Hints:**
- Use ${} for expressions
- Backticks allow multi-line

**Extension:** Add tagged template literals for custom formatting.

---

### Assignment B11: String Methods I
**Difficulty:** ⭐⭐ (2/5) | **Time:** 25 mins

**Problem Statement:**
Create a string utility library.

**Requirements:**
```javascript
const stringUtils = {
  capitalize(str) { },      // "hello" → "Hello"
  titleCase(str) { },       // "hello world" → "Hello World"
  countWords(str) { },      // "hello world" → 2
  reverse(str) { },         // "hello" → "olleh"
  isPalindrome(str) { },    // "racecar" → true
  truncate(str, len) { },   // Truncate with "..."
};
```

**Test Cases:**
```javascript
stringUtils.capitalize("hello") === "Hello"
stringUtils.titleCase("hello world") === "Hello World"
stringUtils.countWords("  hello   world  ") === 2
stringUtils.reverse("hello") === "olleh"
stringUtils.isPalindrome("A man a plan a canal Panama") === true
stringUtils.truncate("Hello World", 8) === "Hello..."
```

**Learning Objectives:**
- Master common string methods
- Handle edge cases (spaces, case)
- Build reusable utilities

**Hints:**
- Use split(), join(), slice()
- Remember strings are immutable

**Common Mistakes:**
- Not handling whitespace
- Case sensitivity in palindrome

**Extension:** Add methods for slug generation and camelCase conversion.

---

### Assignment B12: String Methods II
**Difficulty:** ⭐⭐ (2/5) | **Time:** 25 mins

**Problem Statement:**
Create a text search and replace utility.

**Requirements:**
```javascript
const textUtils = {
  findAll(text, search) { },      // Return all indices
  replaceAll(text, old, new) { }, // Replace all occurrences
  extractEmails(text) { },        // Find all emails
  extractUrls(text) { },          // Find all URLs
  removeExtraSpaces(text) { },    // Normalize spaces
};
```

**Test Cases:**
```javascript
textUtils.findAll("hello world hello", "hello")
// [0, 12]
textUtils.removeExtraSpaces("  hello   world  ")
// "hello world"
```

**Learning Objectives:**
- Use indexOf, lastIndexOf, includes
- Use replace with patterns
- Build practical text utilities

**Extension:** Add syntax highlighting for code blocks.

---

### Assignment B13: Number Methods
**Difficulty:** ⭐⭐ (2/5) | **Time:** 20 mins

**Problem Statement:**
Create a number formatting utility.

**Requirements:**
```javascript
const numUtils = {
  formatCurrency(num, currency) { },  // 1234.5 → "$1,234.50"
  formatPercent(num, decimals) { },   // 0.856 → "85.60%"
  round(num, decimals) { },           // 3.14159 → 3.14
  isInteger(num) { },                 // 5.0 → true
  inRange(num, min, max) { },         // Check bounds
};
```

**Test Cases:**
```javascript
numUtils.formatCurrency(1234.5, 'USD') === "$1,234.50"
numUtils.formatPercent(0.856, 2) === "85.60%"
numUtils.round(3.14159, 2) === 3.14
numUtils.isInteger(5.0) === true
numUtils.inRange(5, 1, 10) === true
```

**Learning Objectives:**
- Use toFixed, toPrecision
- Use Number.isInteger, isNaN
- Format numbers for display

**Extension:** Add scientific notation and ordinal formatting.

---

### Assignment B14: Scope Detective
**Difficulty:** ⭐⭐ (2/5) | **Time:** 25 mins

**Problem Statement:**
Predict the output of various scope scenarios.

**Requirements:**
Analyze and explain each:
```javascript
// Scenario 1: var vs let in loops
for (var i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 100);
}

for (let j = 0; j < 3; j++) {
  setTimeout(() => console.log(j), 100);
}

// Scenario 2: Block scope
{
  var a = 1;
  let b = 2;
  const c = 3;
}
console.log(a); // ?
console.log(b); // ?

// Scenario 3: Function scope
function outer() {
  var x = 10;
  function inner() {
    console.log(x);
  }
  return inner;
}
```

**Learning Objectives:**
- Understand var's function scope
- Understand let/const block scope
- Recognize scope leakage issues

**Extension:** Create examples showing temporal dead zone.

---

### Assignment B15: Hoisting Explorer
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 30 mins

**Problem Statement:**
Predict outputs and explain hoisting behavior.

**Requirements:**
```javascript
// What is logged? Why?

console.log(a);
var a = 5;

console.log(b);
let b = 5;

console.log(myFunc());
function myFunc() { return "Hello"; }

console.log(myArrow());
var myArrow = () => "Hello";

console.log(MyClass);
class MyClass {}
```

**Learning Objectives:**
- Understand hoisting mechanism
- Know what gets hoisted
- Avoid hoisting pitfalls

**Hints:**
- var declarations hoisted, not initializations
- let/const have temporal dead zone
- Function declarations fully hoisted

**Extension:** Explain how modules affect hoisting.

---

## Module 2: Control Structures

### Assignment B16: If-Else Mastery
**Difficulty:** ⭐ (1/5) | **Time:** 15 mins

**Problem Statement:**
Create a ticket pricing system.

**Requirements:**
```javascript
function getTicketPrice(age, isStudent, dayOfWeek) {
  // Base price: $12
  // Under 12 or over 65: 50% discount
  // Students: 20% discount
  // Tuesday: $5 flat rate
  // Discounts don't stack, use best one
}
```

**Test Cases:**
```javascript
getTicketPrice(10, false, 'Monday') === 6    // Child discount
getTicketPrice(25, true, 'Monday') === 9.6   // Student discount
getTicketPrice(30, false, 'Tuesday') === 5   // Tuesday special
getTicketPrice(70, true, 'Monday') === 6     // Senior (best discount)
```

**Learning Objectives:**
- Structure complex conditions
- Handle multiple discount scenarios
- Return correct values

**Extension:** Add membership tiers with additional discounts.

---

### Assignment B17: Switch Statement
**Difficulty:** ⭐⭐ (2/5) | **Time:** 20 mins

**Problem Statement:**
Create a command interpreter using switch.

**Requirements:**
```javascript
function executeCommand(command, ...args) {
  // Commands: "add", "subtract", "multiply", "divide"
  // "uppercase", "lowercase", "reverse"
  // "help" - return available commands
  // Unknown command - return error message
}
```

**Test Cases:**
```javascript
executeCommand("add", 5, 3) === 8
executeCommand("uppercase", "hello") === "HELLO"
executeCommand("help") // Returns command list
executeCommand("unknown") // "Unknown command: unknown"
```

**Learning Objectives:**
- Use switch for command routing
- Handle fall-through cases
- Provide default handling

**Common Mistakes:**
- Forgetting break statements
- Not handling default case

**Extension:** Add case-insensitive command matching.

---

### Assignment B18: For Loop Patterns
**Difficulty:** ⭐⭐ (2/5) | **Time:** 25 mins

**Problem Statement:**
Create pattern generators using for loops.

**Requirements:**
```javascript
function printTriangle(n, char = '*') { }
function printPyramid(n, char = '*') { }
function printDiamond(n, char = '*') { }
function printHollowSquare(n, char = '*') { }
```

**Expected Output (n=5):**
```
Triangle:       Pyramid:        Diamond:
*                   *             *
**                 ***           ***
***               *****         *****
****             *******       *******
*****           *********     *********
                              *******
Hollow Square:                 *****
*****                           ***
*   *                            *
*   *
*   *
*****
```

**Learning Objectives:**
- Master nested loops
- Control loop iterations
- Build visual patterns

**Extension:** Add rotation (90°, 180°, 270°) for patterns.

---

### Assignment B19: While Loop Challenges
**Difficulty:** ⭐⭐ (2/5) | **Time:** 20 mins

**Problem Statement:**
Create number analysis functions using while loops.

**Requirements:**
```javascript
function sumDigits(num) { }           // 123 → 6
function reverseNumber(num) { }       // 123 → 321
function countDigits(num) { }         // 123 → 3
function digitalRoot(num) { }         // 123 → 6, 999 → 9
function isPalindrome(num) { }        // 121 → true
```

**Test Cases:**
```javascript
sumDigits(12345) === 15
reverseNumber(12345) === 54321
countDigits(12345) === 5
digitalRoot(99999) === 9
isPalindrome(12321) === true
```

**Learning Objectives:**
- Use while for unknown iterations
- Digit manipulation techniques
- Build upon previous results

**Extension:** Handle negative numbers appropriately.

---

### Assignment B20: Do-While Applications
**Difficulty:** ⭐⭐ (2/5) | **Time:** 20 mins

**Problem Statement:**
Create a menu-driven calculator simulator.

**Requirements:**
```javascript
function menuSimulator() {
  // Simulate a menu that:
  // 1. Shows options
  // 2. Gets "user input" (parameter or mock)
  // 3. Performs action
  // 4. Continues until "exit"
  // Return history of actions
}
```

**Learning Objectives:**
- Understand do-while use case
- Execute at least once pattern
- Handle repeated operations

**Extension:** Add undo functionality for operations.

---

### Assignment B21: For...In Object Iteration
**Difficulty:** ⭐⭐ (2/5) | **Time:** 20 mins

**Problem Statement:**
Create an object inspection utility.

**Requirements:**
```javascript
function inspectObject(obj) {
  // Return:
  // - All own properties
  // - All inherited properties (separate)
  // - Property values and types
}

function compareObjects(obj1, obj2) {
  // Return added, removed, and modified properties
}
```

**Test Cases:**
```javascript
const result = compareObjects(
  { a: 1, b: 2, c: 3 },
  { a: 1, b: 5, d: 4 }
);
// added: ['d'], removed: ['c'], modified: ['b']
```

**Learning Objectives:**
- Use for...in correctly
- Distinguish own vs inherited
- Compare object structures

**Common Mistakes:**
- Not using hasOwnProperty
- Iterating arrays with for...in

**Extension:** Add deep comparison capability.

---

### Assignment B22: For...Of Iteration
**Difficulty:** ⭐⭐ (2/5) | **Time:** 20 mins

**Problem Statement:**
Create iterable processing utilities.

**Requirements:**
```javascript
function processIterable(iterable) {
  // Works with: arrays, strings, maps, sets
  // Return: first, last, count, unique values
}

function zipIterables(...iterables) {
  // Combine multiple iterables
  // zip([1,2], ['a','b']) → [[1,'a'], [2,'b']]
}
```

**Test Cases:**
```javascript
processIterable([1, 2, 2, 3, 3, 3])
// { first: 1, last: 3, count: 6, unique: [1, 2, 3] }

zipIterables([1, 2, 3], ['a', 'b', 'c'])
// [[1, 'a'], [2, 'b'], [3, 'c']]
```

**Learning Objectives:**
- Use for...of with iterables
- Handle different iterable types
- Combine iterables creatively

**Extension:** Create an unzip function.

---

### Assignment B23: Loop Control
**Difficulty:** ⭐⭐ (2/5) | **Time:** 20 mins

**Problem Statement:**
Implement search algorithms using break/continue.

**Requirements:**
```javascript
function findFirst(arr, predicate) { }     // Use break
function findAll(arr, predicate) { }       // No skipping
function findAllExcept(arr, excludePred) { } // Use continue
function findInNested(arr2d, target) { }   // Labeled break
```

**Test Cases:**
```javascript
findFirst([1,2,3,4,5], x => x > 3) === 4
findAll([1,2,3,4,5], x => x % 2 === 0) // [2, 4]
findInNested([[1,2],[3,4],[5,6]], 4) // { row: 1, col: 1 }
```

**Learning Objectives:**
- Use break and continue effectively
- Understand labeled statements
- Optimize searches with early exit

**Extension:** Implement binary search with loop control.

---

### Assignment B24: Nested Loop Challenges
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 30 mins

**Problem Statement:**
Create a multiplication table generator and matrix operations.

**Requirements:**
```javascript
function multiplicationTable(n) { }        // n×n table
function spiralMatrix(n) { }               // Generate spiral
function rotateMatrix(matrix, degrees) { } // 90, 180, 270
function transposeMatrix(matrix) { }       // Rows ↔ Columns
```

**Expected Output (n=3):**
```
Multiplication:     Spiral:
1  2  3             1  2  3
2  4  6             8  9  4
3  6  9             7  6  5
```

**Learning Objectives:**
- Master nested loop patterns
- 2D array manipulation
- Index calculations

**Extension:** Implement matrix multiplication.

---

### Assignment B25: FizzBuzz Variations
**Difficulty:** ⭐⭐ (2/5) | **Time:** 25 mins

**Problem Statement:**
Implement FizzBuzz with multiple variations.

**Requirements:**
```javascript
function classicFizzBuzz(n) { }           // Standard
function customFizzBuzz(n, rules) { }     // Custom rules
function fizzBuzzSum(n) { }               // Sum of non-FB numbers
function fizzBuzzArray(n) { }             // Return array
```

**Test Cases:**
```javascript
customFizzBuzz(15, [[3,'Fizz'], [5,'Buzz'], [7,'Bazz']])
// At 105: "FizzBuzzBazz"

fizzBuzzSum(15) === 1+2+4+7+8+11+13+14 === 60
```

**Learning Objectives:**
- Implement classic algorithm
- Extend with flexibility
- Handle multiple conditions

**Extension:** Create a FizzBuzz that handles prime numbers.

---

### Assignment B26: Number Classification
**Difficulty:** ⭐⭐ (2/5) | **Time:** 25 mins

**Problem Statement:**
Create a number classifier.

**Requirements:**
```javascript
function classifyNumber(n) {
  // Return object with:
  // - isEven, isOdd
  // - isPrime
  // - isPerfect (sum of divisors = n, e.g., 6, 28)
  // - isArmstrong (e.g., 153 = 1³+5³+3³)
  // - factors
}
```

**Test Cases:**
```javascript
classifyNumber(28)
// { isEven: true, isPerfect: true, isPrime: false,
//   isArmstrong: false, factors: [1,2,4,7,14] }
```

**Learning Objectives:**
- Implement mathematical checks
- Combine multiple algorithms
- Build comprehensive analysis

**Extension:** Add Fibonacci check and factorial calculation.

---

### Assignment B27: Prime Number Operations
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 30 mins

**Problem Statement:**
Create a prime number toolkit.

**Requirements:**
```javascript
function isPrime(n) { }                    // Check primality
function nthPrime(n) { }                   // Find nth prime
function primesInRange(start, end) { }     // All primes in range
function primeFactors(n) { }               // Prime factorization
function nextPrime(n) { }                  // Next prime after n
```

**Test Cases:**
```javascript
nthPrime(10) === 29
primesInRange(10, 30) // [11, 13, 17, 19, 23, 29]
primeFactors(84) // [2, 2, 3, 7]
nextPrime(10) === 11
```

**Learning Objectives:**
- Optimize primality testing
- Generate primes efficiently
- Understand factorization

**Hints:**
- Only check up to √n
- Skip even numbers after 2

**Extension:** Implement Sieve of Eratosthenes.

---

### Assignment B28: Input Validation
**Difficulty:** ⭐⭐ (2/5) | **Time:** 25 mins

**Problem Statement:**
Create a form validation system.

**Requirements:**
```javascript
const validators = {
  isEmail(str) { },
  isPhone(str) { },           // Various formats
  isStrongPassword(str) { },  // 8+ chars, upper, lower, number, special
  isUrl(str) { },
  isDate(str) { },            // YYYY-MM-DD format
  isInRange(num, min, max) { },
};
```

**Test Cases:**
```javascript
validators.isEmail("test@example.com") === true
validators.isPhone("(123) 456-7890") === true
validators.isStrongPassword("Abc123!@#") === true
validators.isDate("2024-02-29") === true  // Leap year!
```

**Learning Objectives:**
- Implement validation logic
- Handle format variations
- Consider edge cases

**Extension:** Add custom error messages for each validation failure.

---

### Assignment B29: Grade Calculator
**Difficulty:** ⭐⭐ (2/5) | **Time:** 20 mins

**Problem Statement:**
Create a comprehensive grade calculator.

**Requirements:**
```javascript
function calculateGrades(students) {
  // Input: [{ name, scores: [test1, test2, test3, ...] }]
  // Output for each:
  // - average, letter grade (A-F)
  // - highest, lowest score
  // - pass/fail status (60+ to pass)
  // - class statistics (mean, median, std deviation)
}
```

**Test Cases:**
```javascript
calculateGrades([
  { name: "Alice", scores: [85, 90, 88] },
  { name: "Bob", scores: [72, 68, 75] }
])
// Returns detailed analysis for each + class stats
```

**Learning Objectives:**
- Process data collections
- Calculate statistics
- Format output clearly

**Extension:** Add curve grading option.

---

### Assignment B30: Loop Optimization
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 30 mins

**Problem Statement:**
Optimize inefficient loop code.

**Requirements:**
Refactor each for better performance:
```javascript
// 1. Repeated calculation in condition
for (let i = 0; i < arr.length; i++) { }

// 2. Unnecessary inner loop
for (let i = 0; i < arr.length; i++) {
  for (let j = 0; j < arr.length; j++) {
    if (arr[i] === arr[j] && i !== j) { /* found duplicate */ }
  }
}

// 3. Multiple array iterations
const evens = arr.filter(x => x % 2 === 0);
const doubled = evens.map(x => x * 2);
const sum = doubled.reduce((a, b) => a + b, 0);
```

**Learning Objectives:**
- Cache loop conditions
- Reduce time complexity
- Use appropriate data structures

**Extension:** Benchmark before/after performance.

---

## Module 3: Functions and Scope

### Assignment B31: Function Declarations vs Expressions
**Difficulty:** ⭐⭐ (2/5) | **Time:** 20 mins

**Problem Statement:**
Demonstrate the differences between function types.

**Requirements:**
```javascript
// Implement each as declaration, expression, and arrow:
function addDeclaration(a, b) { }
const addExpression = function(a, b) { };
const addArrow = (a, b) => { };

// Show hoisting differences
console.log(hoistedFunc()); // Works
console.log(hoistedExpr()); // Error
function hoistedFunc() { return "I'm hoisted"; }
var hoistedExpr = function() { return "Not hoisted"; };
```

**Learning Objectives:**
- Understand three function syntaxes
- Know hoisting differences
- Choose appropriate syntax

**Extension:** Compare `this` binding in each type.

---

### Assignment B32: Arrow Functions
**Difficulty:** ⭐⭐ (2/5) | **Time:** 20 mins

**Problem Statement:**
Convert traditional functions to arrow functions.

**Requirements:**
```javascript
// Convert each to arrow functions:
function double(x) { return x * 2; }
function greet(name) { return "Hello, " + name; }
function sum(arr) { return arr.reduce(function(a, b) { return a + b; }, 0); }
function getFullName(person) {
  return person.firstName + " " + person.lastName;
}
```

**Learning Objectives:**
- Master arrow function syntax
- Use implicit returns
- Understand concise body syntax

**Common Mistakes:**
- Forgetting parentheses for objects
- Using arrow functions for methods

**Extension:** Show when NOT to use arrow functions.

---

### Assignment B33: Default Parameters
**Difficulty:** ⭐⭐ (2/5) | **Time:** 15 mins

**Problem Statement:**
Create functions with smart default values.

**Requirements:**
```javascript
function createUser(
  name = "Anonymous",
  role = "user",
  settings = {}
) { }

function createElement(
  tag = "div",
  content = "",
  attributes = { class: "default" }
) { }

function formatDate(
  date = new Date(),
  format = "YYYY-MM-DD"
) { }
```

**Test Cases:**
```javascript
createUser() // Uses all defaults
createUser("John") // Only overrides name
formatDate(undefined, "DD/MM/YYYY") // Uses current date
```

**Learning Objectives:**
- Set meaningful defaults
- Handle undefined vs null
- Use expressions as defaults

**Extension:** Use previous parameters in later defaults.

---

### Assignment B34: Rest Parameters
**Difficulty:** ⭐⭐ (2/5) | **Time:** 20 mins

**Problem Statement:**
Create flexible functions using rest parameters.

**Requirements:**
```javascript
function sum(...numbers) { }
function average(...numbers) { }
function merge(target, ...sources) { }  // Merge objects
function log(level, ...messages) { }    // Logger with level
function groupBy(key, ...objects) { }   // Group by property
```

**Test Cases:**
```javascript
sum(1, 2, 3, 4, 5) === 15
average(10, 20, 30) === 20
merge({a: 1}, {b: 2}, {c: 3}) // {a:1, b:2, c:3}
groupBy('type', {type:'A', v:1}, {type:'B', v:2}, {type:'A', v:3})
// { A: [{...}, {...}], B: [{...}] }
```

**Learning Objectives:**
- Collect variable arguments
- Combine with regular parameters
- Build flexible APIs

**Extension:** Implement function overloading pattern.

---

### Assignment B35: Spread Operator
**Difficulty:** ⭐⭐ (2/5) | **Time:** 20 mins

**Problem Statement:**
Master spread operator usage.

**Requirements:**
```javascript
// Array operations
function combineArrays(...arrays) { }
function insertAt(arr, index, ...items) { }
function removeAt(arr, index, count) { }  // Return new array

// Object operations
function shallowClone(obj) { }
function mergeWithOverride(...objects) { }
function omitKeys(obj, ...keys) { }
```

**Test Cases:**
```javascript
combineArrays([1,2], [3,4], [5,6]) // [1,2,3,4,5,6]
insertAt([1,2,5,6], 2, 3, 4) // [1,2,3,4,5,6]
omitKeys({a:1, b:2, c:3}, 'b', 'c') // {a:1}
```

**Learning Objectives:**
- Spread arrays and objects
- Create immutable operations
- Combine rest and spread

**Extension:** Create a deep merge function.

---

### Assignment B36: Return Values & Side Effects
**Difficulty:** ⭐⭐ (2/5) | **Time:** 25 mins

**Problem Statement:**
Identify and refactor functions with side effects.

**Requirements:**
```javascript
// Identify the side effects in each function:
let counter = 0;
function incrementCounter() { counter++; return counter; }

function addToArray(arr, item) { arr.push(item); return arr; }

function updateUser(user, updates) {
  Object.assign(user, updates);
  console.log("User updated!");
  return user;
}

// Refactor each to be pure:
function pureIncrementCounter(counter) { }
function pureAddToArray(arr, item) { }
function pureUpdateUser(user, updates) { }
```

**Learning Objectives:**
- Identify side effects
- Write pure functions
- Understand predictability benefits

**Extension:** Create a wrapper to log all function calls without side effects.

---

### Assignment B37: Closures Basics
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 30 mins

**Problem Statement:**
Create useful closures.

**Requirements:**
```javascript
function createCounter(start = 0) {
  // Return object with: increment, decrement, getValue, reset
}

function createSecretHolder(secret) {
  // Return object with: getSecret, setSecret
  // Secret should be private
}

function once(fn) {
  // Return function that only executes fn once
  // Subsequent calls return first result
}
```

**Test Cases:**
```javascript
const counter = createCounter(10);
counter.increment(); // 11
counter.getValue(); // 11

const onceAdd = once((a, b) => a + b);
onceAdd(2, 3); // 5
onceAdd(4, 5); // 5 (still returns first result)
```

**Learning Objectives:**
- Understand closure scope
- Create private state
- Build practical utilities

**Extension:** Create a createStack function using closures.

---

### Assignment B38: Higher-Order Functions
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 30 mins

**Problem Statement:**
Implement common higher-order functions from scratch.

**Requirements:**
```javascript
function myMap(arr, callback) { }
function myFilter(arr, callback) { }
function myReduce(arr, callback, initial) { }
function myFind(arr, callback) { }
function myEvery(arr, callback) { }
function mySome(arr, callback) { }
```

**Test Cases:**
```javascript
myMap([1, 2, 3], x => x * 2) // [2, 4, 6]
myFilter([1, 2, 3, 4, 5], x => x % 2 === 0) // [2, 4]
myReduce([1, 2, 3, 4], (a, b) => a + b, 0) // 10
myFind([1, 2, 3, 4], x => x > 2) // 3
```

**Learning Objectives:**
- Understand function as arguments
- Implement iteration patterns
- Handle edge cases

**Extension:** Add index and array parameters to callbacks.

---

### Assignment B39: Callback Functions
**Difficulty:** ⭐⭐ (2/5) | **Time:** 25 mins

**Problem Statement:**
Create a task runner using callbacks.

**Requirements:**
```javascript
function runTasks(tasks, onComplete, onError) {
  // tasks: array of functions
  // Execute each task in sequence
  // Call onComplete with results when all done
  // Call onError if any task throws
}

function retry(fn, attempts, onSuccess, onFailure) {
  // Try to execute fn up to 'attempts' times
  // Call onSuccess with result if successful
  // Call onFailure with last error if all attempts fail
}
```

**Test Cases:**
```javascript
runTasks([
  () => 1 + 1,
  () => 2 * 2,
  () => 3 ** 3
], results => console.log(results)); // [2, 4, 27]
```

**Learning Objectives:**
- Pass functions as callbacks
- Handle success and error cases
- Chain operations

**Extension:** Add timeout handling for long-running tasks.

---

### Assignment B40: IIFE Patterns
**Difficulty:** ⭐⭐ (2/5) | **Time:** 20 mins

**Problem Statement:**
Implement the module pattern using IIFE.

**Requirements:**
```javascript
const Calculator = (function() {
  // Private state and methods
  // Public API: add, subtract, multiply, divide, getHistory, clear
})();

const Counter = (function(initial) {
  // Private count
  // Public: increment, decrement, getValue
})(0);
```

**Test Cases:**
```javascript
Calculator.add(5, 3); // 8
Calculator.getHistory(); // [{op: 'add', args: [5,3], result: 8}]

Counter.increment();
Counter.getValue(); // 1
```

**Learning Objectives:**
- Create private scope with IIFE
- Expose public API
- Initialize with parameters

**Extension:** Create a plugin system using IIFE.

---

### Assignment B41: Recursion Basics
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 30 mins

**Problem Statement:**
Implement classic recursive algorithms.

**Requirements:**
```javascript
function factorial(n) { }
function fibonacci(n) { }
function sumArray(arr) { }           // Recursive sum
function deepFlatten(arr) { }        // Flatten nested arrays
function countDown(n) { }            // Return countdown array
function power(base, exp) { }        // Without ** operator
```

**Test Cases:**
```javascript
factorial(5) === 120
fibonacci(10) === 55
sumArray([1, [2, [3, [4]]]]) === 10
deepFlatten([1, [2, [3, [4, [5]]]]]) // [1, 2, 3, 4, 5]
power(2, 10) === 1024
```

**Learning Objectives:**
- Identify base cases
- Build recursive logic
- Handle nested structures

**Common Mistakes:**
- Forgetting base case (infinite recursion)
- Not returning recursive call results

**Extension:** Add memoization to optimize fibonacci.

---

### Assignment B42: Advanced Recursion
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 35 mins

**Problem Statement:**
Solve complex problems recursively.

**Requirements:**
```javascript
function deepClone(obj) { }          // Deep copy any structure
function permutations(arr) { }       // All permutations
function combinations(arr, k) { }    // k-combinations
function pathsInGrid(m, n) { }       // Count paths in m×n grid
function towerOfHanoi(n, from, to, aux) { } // Return moves array
```

**Test Cases:**
```javascript
permutations([1, 2, 3])
// [[1,2,3], [1,3,2], [2,1,3], [2,3,1], [3,1,2], [3,2,1]]
combinations([1, 2, 3, 4], 2)
// [[1,2], [1,3], [1,4], [2,3], [2,4], [3,4]]
pathsInGrid(3, 3) === 6
```

**Learning Objectives:**
- Complex recursive patterns
- Backtracking concepts
- Build solution incrementally

**Extension:** Implement recursive tree traversal.

---

### Assignment B43: Function Composition
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 25 mins

**Problem Statement:**
Create function composition utilities.

**Requirements:**
```javascript
function compose(...fns) {
  // Returns function that applies fns right to left
  // compose(f, g, h)(x) = f(g(h(x)))
}

function pipe(...fns) {
  // Returns function that applies fns left to right
  // pipe(f, g, h)(x) = h(g(f(x)))
}

// Usage example:
const processUser = pipe(
  trim,
  lowercase,
  validateEmail,
  saveToDatabase
);
```

**Test Cases:**
```javascript
const double = x => x * 2;
const addOne = x => x + 1;
compose(double, addOne)(5) // 12 (addOne then double)
pipe(double, addOne)(5)    // 11 (double then addOne)
```

**Learning Objectives:**
- Compose small functions
- Build data pipelines
- Create reusable transformations

**Extension:** Add async composition support.

---

### Assignment B44: Currying
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 25 mins

**Problem Statement:**
Implement and use currying.

**Requirements:**
```javascript
function curry(fn) {
  // Transform fn into curried version
  // curry(add)(1)(2)(3) = add(1, 2, 3)
}

// Create curried utilities:
const add = curry((a, b, c) => a + b + c);
const format = curry((template, ...values) => { });
const log = curry((level, timestamp, message) => { });
```

**Test Cases:**
```javascript
const add = curry((a, b, c) => a + b + c);
add(1)(2)(3) === 6
add(1, 2)(3) === 6
add(1)(2, 3) === 6
add(1, 2, 3) === 6
```

**Learning Objectives:**
- Understand currying concept
- Create partial application
- Build configurable functions

**Extension:** Implement placeholder support for argument positions.

---

### Assignment B45: Method Chaining
**Difficulty:** ⭐⭐ (2/5) | **Time:** 25 mins

**Problem Statement:**
Create a chainable string builder.

**Requirements:**
```javascript
class StringBuilder {
  // Chainable methods:
  // append(str), prepend(str), trim()
  // toUpperCase(), toLowerCase(), capitalize()
  // replace(old, new), reverse()
  // repeat(times), toString()
}
```

**Test Cases:**
```javascript
const result = new StringBuilder("hello")
  .append(" world")
  .toUpperCase()
  .append("!")
  .toString();
// "HELLO WORLD!"

new StringBuilder("  test  ")
  .trim()
  .capitalize()
  .repeat(2)
  .toString();
// "TestTest"
```

**Learning Objectives:**
- Return `this` for chaining
- Build fluent interfaces
- Maintain immutability option

**Extension:** Add undo functionality to the chain.

---

## Module 4: Arrays, Objects, and Strings

### Assignment B46: Array Basics
**Difficulty:** ⭐ (1/5) | **Time:** 20 mins

**Problem Statement:**
Create an array management utility.

**Requirements:**
```javascript
const arrayManager = {
  create(...items) { },         // Create array from arguments
  addToEnd(arr, item) { },      // push behavior, return new array
  addToStart(arr, item) { },    // unshift behavior, return new array
  removeFromEnd(arr) { },       // pop behavior, return [newArr, removed]
  removeFromStart(arr) { },     // shift behavior, return [newArr, removed]
  getLength(arr) { },
  isEmpty(arr) { },
};
```

**Test Cases:**
```javascript
arrayManager.create(1, 2, 3) // [1, 2, 3]
arrayManager.addToEnd([1, 2], 3) // [1, 2, 3]
arrayManager.removeFromEnd([1, 2, 3]) // [[1, 2], 3]
arrayManager.isEmpty([]) === true
```

**Learning Objectives:**
- Master basic array operations
- Understand mutating vs non-mutating approaches
- Return useful results

**Extension:** Add insertAt and removeAt methods.

---

### Assignment B47: Array Slice and Splice
**Difficulty:** ⭐⭐ (2/5) | **Time:** 25 mins

**Problem Statement:**
Master slice and splice differences.

**Requirements:**
```javascript
const slicer = {
  getSubarray(arr, start, end) { },     // Using slice
  getFirstN(arr, n) { },
  getLastN(arr, n) { },
  removeMiddle(arr, start, count) { },  // Using splice
  insertMiddle(arr, index, ...items) { },
  replaceRange(arr, start, count, ...items) { },
};
```

**Test Cases:**
```javascript
slicer.getSubarray([1,2,3,4,5], 1, 4) // [2, 3, 4]
slicer.getLastN([1,2,3,4,5], 2) // [4, 5]
slicer.removeMiddle([1,2,3,4,5], 2, 2) // [1, 2, 5]
slicer.insertMiddle([1,2,5,6], 2, 3, 4) // [1,2,3,4,5,6]
```

**Learning Objectives:**
- Know slice is non-mutating
- Know splice mutates original
- Handle negative indices

**Common Mistakes:**
- Confusing slice and splice
- Not handling negative indices correctly

**Extension:** Create an immutable splice that returns new array.

---

### Assignment B48: Array Search Methods
**Difficulty:** ⭐⭐ (2/5) | **Time:** 20 mins

**Problem Statement:**
Implement search operations on arrays.

**Requirements:**
```javascript
const searcher = {
  findIndex(arr, value) { },       // indexOf behavior
  findLastIndex(arr, value) { },   // lastIndexOf behavior
  contains(arr, value) { },        // includes behavior
  findAllIndices(arr, value) { },  // All occurrences
  findByCondition(arr, fn) { },    // find behavior
};
```

**Test Cases:**
```javascript
searcher.findIndex([1,2,3,2,1], 2) === 1
searcher.findLastIndex([1,2,3,2,1], 2) === 3
searcher.findAllIndices([1,2,3,2,1], 2) // [1, 3]
searcher.findByCondition([1,2,3,4,5], x => x > 3) // 4
```

**Learning Objectives:**
- Use indexOf, lastIndexOf, includes
- Implement custom search logic
- Handle not-found cases

**Extension:** Add fuzzy search capability.

---

### Assignment B49: Array Transformation
**Difficulty:** ⭐⭐ (2/5) | **Time:** 25 mins

**Problem Statement:**
Transform arrays in various ways.

**Requirements:**
```javascript
const transformer = {
  double(arr) { },              // Double all numbers
  square(arr) { },              // Square all numbers
  toStrings(arr) { },           // Convert all to strings
  toUpperCase(arr) { },         // Uppercase all strings
  extractProperty(arr, key) { }, // Get property from objects
  applyFunction(arr, fn) { },   // Apply custom function
};
```

**Test Cases:**
```javascript
transformer.double([1, 2, 3]) // [2, 4, 6]
transformer.extractProperty(
  [{name: 'Alice'}, {name: 'Bob'}], 
  'name'
) // ['Alice', 'Bob']
```

**Learning Objectives:**
- Use map for transformations
- Create reusable transformers
- Handle different data types

**Extension:** Create chainable transformations.

---

### Assignment B50: Array Filtering
**Difficulty:** ⭐⭐ (2/5) | **Time:** 20 mins

**Problem Statement:**
Filter arrays with various conditions.

**Requirements:**
```javascript
const filters = {
  evens(arr) { },
  odds(arr) { },
  positives(arr) { },
  truthy(arr) { },
  unique(arr) { },
  byProperty(arr, key, value) { },
  byRange(arr, min, max) { },
};
```

**Test Cases:**
```javascript
filters.evens([1,2,3,4,5,6]) // [2, 4, 6]
filters.unique([1,2,2,3,3,3]) // [1, 2, 3]
filters.byRange([1,5,10,15,20], 5, 15) // [5, 10, 15]
```

**Learning Objectives:**
- Use filter method effectively
- Combine multiple conditions
- Create reusable filters

**Extension:** Add negation helpers (notEvens, notInRange).

---

### Assignment B51: Array Aggregation
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 30 mins

**Problem Statement:**
Aggregate array data using reduce.

**Requirements:**
```javascript
const aggregator = {
  sum(arr) { },
  product(arr) { },
  average(arr) { },
  min(arr) { },
  max(arr) { },
  countOccurrences(arr) { },    // { value: count }
  groupBy(arr, key) { },        // Group objects by key
  partition(arr, fn) { },       // Split into [truthy, falsy]
};
```

**Test Cases:**
```javascript
aggregator.countOccurrences(['a','b','a','c','a']) 
// { a: 3, b: 1, c: 1 }
aggregator.partition([1,2,3,4,5], x => x > 3)
// [[4, 5], [1, 2, 3]]
```

**Learning Objectives:**
- Master reduce method
- Build complex aggregations
- Return useful structures

**Extension:** Implement running sum/average.

---

### Assignment B52: Array Sorting
**Difficulty:** ⭐⭐ (2/5) | **Time:** 25 mins

**Problem Statement:**
Sort arrays with custom comparators.

**Requirements:**
```javascript
const sorter = {
  ascending(arr) { },
  descending(arr) { },
  alphabetical(arr) { },
  byProperty(arr, key, order) { },
  byMultipleKeys(arr, keys) { },
  stable(arr, compareFn) { },
};
```

**Test Cases:**
```javascript
sorter.ascending([3, 1, 4, 1, 5]) // [1, 1, 3, 4, 5]
sorter.byProperty(
  [{age: 25}, {age: 20}, {age: 30}],
  'age', 
  'asc'
) // [{age: 20}, {age: 25}, {age: 30}]
```

**Learning Objectives:**
- Write custom compare functions
- Handle numeric vs string sorting
- Maintain stability when needed

**Common Mistakes:**
- Default sort converts to strings
- Mutating original array

**Extension:** Implement shuffle (Fisher-Yates).

---

### Assignment B53: Object Basics
**Difficulty:** ⭐⭐ (2/5) | **Time:** 20 mins

**Problem Statement:**
Master object creation and access.

**Requirements:**
```javascript
const objectUtils = {
  create(pairs) { },             // From key-value pairs
  get(obj, path) { },            // Dot notation path "a.b.c"
  set(obj, path, value) { },     // Set nested property
  has(obj, key) { },             // Check property exists
  getKeys(obj) { },
  getValues(obj) { },
  getEntries(obj) { },
};
```

**Test Cases:**
```javascript
objectUtils.get({a: {b: {c: 5}}}, 'a.b.c') === 5
objectUtils.set({}, 'a.b.c', 5) // {a: {b: {c: 5}}}
objectUtils.has({a: undefined}, 'a') === true
```

**Learning Objectives:**
- Access nested properties
- Create objects dynamically
- Handle missing properties

**Extension:** Add support for array indices in paths.

---

### Assignment B54: Object Manipulation
**Difficulty:** ⭐⭐ (2/5) | **Time:** 25 mins

**Problem Statement:**
Manipulate object structures.

**Requirements:**
```javascript
const objManipulator = {
  pick(obj, keys) { },           // Select keys
  omit(obj, keys) { },           // Exclude keys
  rename(obj, keyMap) { },       // Rename keys
  mapValues(obj, fn) { },        // Transform values
  mapKeys(obj, fn) { },          // Transform keys
  invert(obj) { },               // Swap keys and values
};
```

**Test Cases:**
```javascript
objManipulator.pick({a:1, b:2, c:3}, ['a', 'c']) // {a:1, c:3}
objManipulator.rename({name: 'John'}, {name: 'firstName'})
// {firstName: 'John'}
objManipulator.invert({a: 1, b: 2}) // {1: 'a', 2: 'b'}
```

**Learning Objectives:**
- Transform object structures
- Create new objects immutably
- Handle edge cases

**Extension:** Add merge with conflict resolution.

---

### Assignment B55: Object Comparison
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 30 mins

**Problem Statement:**
Compare objects deeply.

**Requirements:**
```javascript
const comparator = {
  shallowEqual(obj1, obj2) { },
  deepEqual(obj1, obj2) { },
  diff(obj1, obj2) { },          // Return differences
  isSubset(subset, obj) { },
  merge(obj1, obj2, strategy) { }, // 'overwrite' | 'keepOld' | 'merge'
};
```

**Test Cases:**
```javascript
comparator.deepEqual(
  {a: {b: 1}}, 
  {a: {b: 1}}
) === true

comparator.diff(
  {a: 1, b: 2, c: 3},
  {a: 1, b: 5, d: 4}
) // { added: ['d'], removed: ['c'], changed: ['b'] }
```

**Learning Objectives:**
- Implement deep comparison
- Track object differences
- Handle nested structures

**Extension:** Add circular reference handling.

---

### Assignment B56: JSON Operations
**Difficulty:** ⭐⭐ (2/5) | **Time:** 20 mins

**Problem Statement:**
Work with JSON data.

**Requirements:**
```javascript
const jsonUtils = {
  parse(str, reviver) { },
  stringify(obj, replacer, space) { },
  clone(obj) { },                // Deep clone via JSON
  isValid(str) { },              // Check if valid JSON
  prettify(str) { },             // Format JSON string
  minify(str) { },               // Remove whitespace
};
```

**Test Cases:**
```javascript
jsonUtils.isValid('{"name": "John"}') === true
jsonUtils.isValid('{name: "John"}') === false
jsonUtils.prettify('{"a":1,"b":2}')
// '{\n  "a": 1,\n  "b": 2\n}'
```

**Learning Objectives:**
- Use JSON.parse and stringify
- Handle parse errors gracefully
- Create custom serialization

**Common Mistakes:**
- Not handling parse errors
- Losing Date and undefined values

**Extension:** Implement reviver for Date restoration.

---

### Assignment B57: String Builder Advanced
**Difficulty:** ⭐⭐ (2/5) | **Time:** 25 mins

**Problem Statement:**
Create an advanced string processor.

**Requirements:**
```javascript
const stringProcessor = {
  padLeft(str, len, char) { },
  padRight(str, len, char) { },
  center(str, len, char) { },
  wrap(str, width) { },          // Word wrap
  chunk(str, size) { },          // Split into chunks
  mask(str, visibleStart, visibleEnd) { },
};
```

**Test Cases:**
```javascript
stringProcessor.padLeft('5', 3, '0') // "005"
stringProcessor.center('hi', 6, '-') // "--hi--"
stringProcessor.mask('1234567890', 2, 2) // "12******90"
stringProcessor.chunk('abcdefgh', 3) // ['abc', 'def', 'gh']
```

**Learning Objectives:**
- Build complex string utilities
- Handle edge cases
- Create formatters

**Extension:** Add Unicode-aware character counting.

---

### Assignment B58: Array Challenges I
**Difficulty:** ⭐⭐ (2/5) | **Time:** 25 mins

**Problem Statement:**
Solve array manipulation challenges.

**Requirements:**
```javascript
function rotateLeft(arr, positions) { }
function rotateRight(arr, positions) { }
function interleave(arr1, arr2) { }    // [1,2,3], ['a','b','c'] → [1,'a',2,'b',3,'c']
function removeDuplicates(arr) { }      // Maintain order
function intersection(arr1, arr2) { }
function difference(arr1, arr2) { }
```

**Test Cases:**
```javascript
rotateLeft([1,2,3,4,5], 2) // [3,4,5,1,2]
interleave([1,2,3], ['a','b','c']) // [1,'a',2,'b',3,'c']
intersection([1,2,3,4], [3,4,5,6]) // [3, 4]
difference([1,2,3,4], [3,4,5,6]) // [1, 2]
```

**Learning Objectives:**
- Think algorithmically
- Handle array manipulation
- Consider edge cases

**Extension:** Handle arrays of different lengths.

---

### Assignment B59: Array Challenges II
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 30 mins

**Problem Statement:**
Solve more complex array challenges.

**Requirements:**
```javascript
function chunk(arr, size) { }           // Split into size chunks
function flatten(arr, depth) { }        // Flatten to depth
function compact(arr) { }               // Remove falsy values
function zip(...arrays) { }             // Combine arrays
function unzip(arr) { }                 // Reverse of zip
function sample(arr, n) { }             // Random n elements
```

**Test Cases:**
```javascript
chunk([1,2,3,4,5,6,7], 3) // [[1,2,3], [4,5,6], [7]]
flatten([1, [2, [3, [4]]]], 2) // [1, 2, 3, [4]]
zip([1,2], ['a','b'], [true,false])
// [[1,'a',true], [2,'b',false]]
```

**Learning Objectives:**
- Handle complex transformations
- Work with variable inputs
- Build utility functions

**Extension:** Implement flatMap from scratch.

---

### Assignment B60: Object Challenges
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 30 mins

**Problem Statement:**
Solve object manipulation challenges.

**Requirements:**
```javascript
function flattenObject(obj, prefix) { }  // {a:{b:1}} → {'a.b': 1}
function unflattenObject(obj) { }        // Reverse
function deepFreeze(obj) { }             // Recursively freeze
function objectFromPairs(pairs) { }      // [['a',1]] → {a:1}
function toPairs(obj) { }                // {a:1} → [['a',1]]
function defaults(obj, defaults) { }     // Fill missing
```

**Test Cases:**
```javascript
flattenObject({a: {b: {c: 1}}, d: 2})
// { 'a.b.c': 1, 'd': 2 }

unflattenObject({'a.b.c': 1, 'd': 2})
// {a: {b: {c: 1}}, d: 2}
```

**Learning Objectives:**
- Navigate nested structures
- Transform between formats
- Handle recursive operations

**Extension:** Support array notation in paths.

---

## Module 5: Beginner Projects

### Assignment B61: Simple Calculator
**Difficulty:** ⭐⭐ (2/5) | **Time:** 45 mins

**Problem Statement:**
Build a command-line calculator.

**Requirements:**
```javascript
class Calculator {
  // Operations: add, subtract, multiply, divide
  // Memory: store, recall, clear
  // History: getHistory(), undo()
  // Chain calculations
}
```

**Test Cases:**
```javascript
const calc = new Calculator();
calc.add(10).multiply(2).subtract(5).getValue() // 15
calc.store().add(100).recall().getValue() // 15
calc.getHistory() // Shows all operations
```

**Learning Objectives:**
- Combine multiple concepts
- Build complete application
- Implement state management

**Extension:** Add scientific calculator functions.

---

### Assignment B62: Contact Book
**Difficulty:** ⭐⭐ (2/5) | **Time:** 45 mins

**Problem Statement:**
Create a contact management system.

**Requirements:**
```javascript
class ContactBook {
  add(contact) { }           // { name, phone, email }
  remove(name) { }
  find(query) { }            // Search by any field
  update(name, updates) { }
  getAll() { }
  getByGroup(group) { }
  export() { }               // Return JSON
  import(json) { }
}
```

**Test Cases:**
```javascript
const book = new ContactBook();
book.add({ name: 'John', phone: '123', email: 'john@test.com' });
book.find('john') // Returns matching contacts
book.update('John', { phone: '456' });
```

**Learning Objectives:**
- CRUD operations
- Search implementation
- Data persistence format

**Extension:** Add sorting and pagination.

---

### Assignment B63: Todo List (Array-Based)
**Difficulty:** ⭐⭐ (2/5) | **Time:** 40 mins

**Problem Statement:**
Create a todo list using arrays.

**Requirements:**
```javascript
class TodoList {
  add(text, priority = 'medium') { }
  remove(id) { }
  complete(id) { }
  uncomplete(id) { }
  edit(id, newText) { }
  filter(status) { }          // 'all' | 'active' | 'completed'
  sort(by) { }                // 'date' | 'priority' | 'alphabetical'
  clear(status) { }           // Clear completed
}
```

**Test Cases:**
```javascript
const todo = new TodoList();
todo.add('Learn JavaScript', 'high');
todo.add('Build project', 'medium');
todo.complete(1);
todo.filter('completed') // Returns completed items
```

**Learning Objectives:**
- Manage collection data
- Implement status changes
- Filter and sort data

**Extension:** Add due dates and reminders.

---

### Assignment B64: Rock Paper Scissors
**Difficulty:** ⭐⭐ (2/5) | **Time:** 35 mins

**Problem Statement:**
Create Rock Paper Scissors game with stats.

**Requirements:**
```javascript
class RockPaperScissors {
  play(playerChoice) { }      // Returns result
  getStats() { }              // Wins, losses, ties
  getHistory() { }            // Last N games
  reset() { }                 // Reset stats
  // Bonus: predictNext() - Simple AI based on player patterns
}
```

**Test Cases:**
```javascript
const game = new RockPaperScissors();
game.play('rock') // { player: 'rock', computer: '...', result: '...' }
game.getStats() // { wins: 1, losses: 0, ties: 0, winRate: 100% }
```

**Learning Objectives:**
- Game logic implementation
- Random generation
- Statistics tracking

**Extension:** Add Spock-Lizard extension of the game.

---

### Assignment B65: Number Guessing Game
**Difficulty:** ⭐⭐ (2/5) | **Time:** 35 mins

**Problem Statement:**
Create an interactive guessing game.

**Requirements:**
```javascript
class GuessingGame {
  start(min = 1, max = 100) { }
  guess(number) { }            // Returns hint: 'higher' | 'lower' | 'correct'
  getGuessCount() { }
  getHistory() { }
  giveHint() { }               // Narrow the range
  getStats() { }               // Best score, average, games played
}
```

**Test Cases:**
```javascript
const game = new GuessingGame();
game.start(1, 100);
game.guess(50) // "lower"
game.guess(25) // "higher"
game.guess(37) // "correct!"
game.getGuessCount() // 3
```

**Learning Objectives:**
- Game state management
- Binary search concept
- Score tracking

**Extension:** Add difficulty levels and time limits.

---

### Assignment B66: Password Generator
**Difficulty:** ⭐⭐ (2/5) | **Time:** 30 mins

**Problem Statement:**
Create a configurable password generator.

**Requirements:**
```javascript
class PasswordGenerator {
  generate(length, options) { }
  // options: { uppercase, lowercase, numbers, symbols, excludeSimilar }
  generateMultiple(count, length, options) { }
  checkStrength(password) { }  // weak | medium | strong | very strong
  generatePassphrase(wordCount) { }  // Word-based password
}
```

**Test Cases:**
```javascript
const gen = new PasswordGenerator();
gen.generate(12, { uppercase: true, numbers: true }) 
// "Abc123Xyz789" type password
gen.checkStrength("password") // "weak"
gen.checkStrength("P@ssw0rd!123") // "very strong"
```

**Learning Objectives:**
- Random generation
- Character set manipulation
- Security concepts

**Extension:** Add pronounceable password option.

---

### Assignment B67: Temperature Converter
**Difficulty:** ⭐ (1/5) | **Time:** 25 mins

**Problem Statement:**
Create a comprehensive temperature converter.

**Requirements:**
```javascript
class TemperatureConverter {
  celsiusToFahrenheit(c) { }
  fahrenheitToCelsius(f) { }
  celsiusToKelvin(c) { }
  kelvinToCelsius(k) { }
  convert(value, from, to) { } // Generic converter
  // from/to: 'C' | 'F' | 'K'
}
```

**Test Cases:**
```javascript
const conv = new TemperatureConverter();
conv.celsiusToFahrenheit(0) === 32
conv.fahrenheitToCelsius(98.6) // ~37
conv.convert(100, 'C', 'K') === 373.15
```

**Learning Objectives:**
- Mathematical formulas
- Unit conversion logic
- Method organization

**Extension:** Add Rankine and Réaumur scales.

---

### Assignment B68: Palindrome Checker
**Difficulty:** ⭐⭐ (2/5) | **Time:** 30 mins

**Problem Statement:**
Create a comprehensive palindrome checker.

**Requirements:**
```javascript
const palindromeChecker = {
  isSimplePalindrome(str) { },     // Exact match
  isPalindrome(str) { },           // Ignore case, spaces, punctuation
  isPalindromeNumber(num) { },
  longestPalindromeSubstring(str) { },
  makePalindrome(str) { },         // Minimum additions
  allPalindromeSubstrings(str) { },
};
```

**Test Cases:**
```javascript
palindromeChecker.isPalindrome("A man, a plan, a canal: Panama") // true
palindromeChecker.isPalindromeNumber(12321) // true
palindromeChecker.longestPalindromeSubstring("babad") // "bab" or "aba"
```

**Learning Objectives:**
- String manipulation
- Algorithm design
- Handle edge cases

**Extension:** Check for sentence palindromes.

---

### Assignment B69: FizzBuzz Extended
**Difficulty:** ⭐⭐ (2/5) | **Time:** 30 mins

**Problem Statement:**
Create an extensible FizzBuzz implementation.

**Requirements:**
```javascript
class FizzBuzz {
  constructor() {
    this.rules = new Map();
  }
  addRule(divisor, word) { }
  removeRule(divisor) { }
  run(n) { }               // Return array of results
  runRange(start, end) { }
  getStatistics(n) { }     // Count of each output type
}
```

**Test Cases:**
```javascript
const fb = new FizzBuzz();
fb.addRule(3, 'Fizz');
fb.addRule(5, 'Buzz');
fb.addRule(7, 'Bazz');
fb.run(105) // "FizzBuzzBazz" at 105
fb.getStatistics(100) // { Fizz: 22, Buzz: 14, FizzBuzz: 6, numbers: 58 }
```

**Learning Objectives:**
- Configure behavior dynamically
- Use Map data structure
- Calculate statistics

**Extension:** Add rule priority handling.

---

### Assignment B70: Shopping Cart
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 50 mins

**Problem Statement:**
Create a shopping cart with discounts.

**Requirements:**
```javascript
class ShoppingCart {
  addItem(product, quantity) { }
  removeItem(productId) { }
  updateQuantity(productId, quantity) { }
  applyDiscount(code) { }      // Percentage or fixed
  applyCoupon(code) { }        // One-time use
  getSubtotal() { }
  getTax(rate) { }
  getTotal() { }
  checkout() { }               // Return order summary
  clear() { }
}
```

**Test Cases:**
```javascript
const cart = new ShoppingCart();
cart.addItem({ id: 1, name: 'Book', price: 20 }, 2);
cart.addItem({ id: 2, name: 'Pen', price: 5 }, 3);
cart.applyDiscount('SAVE10'); // 10% off
cart.getSubtotal() // 55
cart.getTotal() // 49.50 (after discount)
```

**Learning Objectives:**
- E-commerce logic
- Price calculations
- Discount handling

**Extension:** Add buy-one-get-one and bulk discounts.

---

# 🟡 INTERMEDIATE LEVEL

## Module 1: DOM Manipulation

### Assignment I1: Element Selection
**Difficulty:** ⭐⭐ (2/5) | **Time:** 25 mins

**Problem Statement:**
Create a DOM selection utility library.

**Requirements:**
```javascript
const DOMSelector = {
  byId(id) { },                      // getElementById
  byClass(className) { },            // getElementsByClassName
  byTag(tagName) { },                // getElementsByTagName
  query(selector) { },               // querySelector
  queryAll(selector) { },            // querySelectorAll
  closest(element, selector) { },    // Find ancestor
  parent(element) { },
  children(element) { },
  siblings(element) { },
};
```

**Test Cases:**
```javascript
DOMSelector.byId('header') // Returns element
DOMSelector.queryAll('.card') // Returns NodeList
DOMSelector.siblings(element) // Returns array of siblings
```

**Learning Objectives:**
- Master DOM selection methods
- Understand HTMLCollection vs NodeList
- Navigate DOM relationships

**Extension:** Add filter support for children/siblings.

---

### Assignment I2: Element Creation
**Difficulty:** ⭐⭐ (2/5) | **Time:** 25 mins

**Problem Statement:**
Create a DOM element factory.

**Requirements:**
```javascript
const DOMFactory = {
  create(tag, attributes, children) { },
  createFromHTML(htmlString) { },
  clone(element, deep = true) { },
  fragment(elements) { },            // Create DocumentFragment
  template(templateId, data) { },    // Use <template>
};

// Usage:
DOMFactory.create('div', 
  { class: 'card', id: 'card-1' },
  [
    DOMFactory.create('h2', {}, ['Title']),
    DOMFactory.create('p', {}, ['Content'])
  ]
);
```

**Learning Objectives:**
- Create elements programmatically
- Use DocumentFragment for performance
- Clone and template elements

**Extension:** Add JSX-like syntax support.

---

### Assignment I3: Content Manipulation
**Difficulty:** ⭐⭐ (2/5) | **Time:** 20 mins

**Problem Statement:**
Create utilities for content manipulation.

**Requirements:**
```javascript
const ContentManager = {
  setText(element, text) { },        // textContent
  setHTML(element, html) { },        // innerHTML (with sanitization)
  getText(element) { },
  getHTML(element) { },
  append(parent, child) { },
  prepend(parent, child) { },
  insertBefore(newEl, refEl) { },
  insertAfter(newEl, refEl) { },
  replace(oldEl, newEl) { },
  remove(element) { },
  empty(element) { },                // Remove all children
};
```

**Learning Objectives:**
- Understand textContent vs innerHTML vs innerText
- Insert elements at specific positions
- Safely manipulate content

**Common Mistakes:**
- XSS vulnerabilities with innerHTML
- Not sanitizing user input

**Extension:** Implement a simple HTML sanitizer.

---

### Assignment I4: Attribute Management
**Difficulty:** ⭐⭐ (2/5) | **Time:** 20 mins

**Problem Statement:**
Create an attribute management utility.

**Requirements:**
```javascript
const AttributeManager = {
  get(element, attr) { },
  set(element, attr, value) { },
  remove(element, attr) { },
  has(element, attr) { },
  toggle(element, attr) { },         // Bool attributes
  getAll(element) { },               // Return all as object
  setMultiple(element, attrs) { },   // Set multiple
  getData(element, key) { },         // data-* attributes
  setData(element, key, value) { },
};
```

**Test Cases:**
```javascript
AttributeManager.set(img, 'src', 'image.jpg');
AttributeManager.getData(element, 'userId') // data-user-id
AttributeManager.getAll(element) // { id: '...', class: '...', ... }
```

**Learning Objectives:**
- Work with attributes vs properties
- Use data attributes correctly
- Handle boolean attributes

**Extension:** Add attribute observation with MutationObserver.

---

### Assignment I5: Class Manipulation
**Difficulty:** ⭐⭐ (2/5) | **Time:** 20 mins

**Problem Statement:**
Create a class manipulation library.

**Requirements:**
```javascript
const ClassManager = {
  add(element, ...classes) { },
  remove(element, ...classes) { },
  toggle(element, className, force) { },
  has(element, className) { },
  replace(element, oldClass, newClass) { },
  getAll(element) { },
  clear(element) { },                // Remove all classes
  addConditional(element, className, condition) { },
};
```

**Test Cases:**
```javascript
ClassManager.add(el, 'active', 'visible');
ClassManager.toggle(el, 'dark-mode');
ClassManager.addConditional(el, 'error', isInvalid);
```

**Learning Objectives:**
- Use classList API
- Conditional class toggling
- Multiple class operations

**Extension:** Add animation class helpers.

---

### Assignment I6: Style Manipulation
**Difficulty:** ⭐⭐ (2/5) | **Time:** 25 mins

**Problem Statement:**
Create a style management utility.

**Requirements:**
```javascript
const StyleManager = {
  set(element, property, value) { },
  get(element, property) { },        // Including computed
  setMultiple(element, styles) { },
  getComputed(element, property) { },
  show(element) { },
  hide(element) { },
  toggle(element) { },
  setCSS(element, cssText) { },
  animate(element, keyframes, options) { }, // Web Animations API
};
```

**Test Cases:**
```javascript
StyleManager.set(el, 'backgroundColor', 'blue');
StyleManager.setMultiple(el, { width: '100px', height: '50px' });
StyleManager.getComputed(el, 'display');
```

**Learning Objectives:**
- Set inline styles
- Get computed styles
- Use Web Animations API basics

**Extension:** Add CSS variable manipulation.

---

### Assignment I7: DOM Traversal
**Difficulty:** ⭐⭐ (2/5) | **Time:** 25 mins

**Problem Statement:**
Create a DOM traversal utility.

**Requirements:**
```javascript
const DOMTraversal = {
  parent(element) { },
  parents(element) { },              // All ancestors
  parentsUntil(element, selector) { },
  children(element, selector) { },
  firstChild(element) { },
  lastChild(element) { },
  next(element) { },
  nextAll(element) { },
  prev(element) { },
  prevAll(element) { },
  find(element, selector) { },       // Descendants matching
  filter(elements, selector) { },
};
```

**Test Cases:**
```javascript
DOMTraversal.parents(element) // [parent, grandparent, ...]
DOMTraversal.find(container, '.item') // All .item descendants
```

**Learning Objectives:**
- Navigate DOM tree
- Filter traversal results
- Handle element relationships

**Extension:** Add tree walking with iterator protocol.

---

### Assignment I8: Building a Dynamic List
**Difficulty:** ⭐⭐ (2/5) | **Time:** 35 mins

**Problem Statement:**
Create a dynamic list component.

**Requirements:**
```javascript
class DynamicList {
  constructor(container, options) { }
  addItem(data) { }
  removeItem(id) { }
  updateItem(id, data) { }
  clear() { }
  render(items) { }
  sort(compareFn) { }
  filter(predicate) { }
  search(query) { }
}
```

**Test Cases:**
```javascript
const list = new DynamicList('#my-list', { 
  template: '<li data-id="{{id}}">{{name}}</li>' 
});
list.addItem({ id: 1, name: 'Item 1' });
list.filter(item => item.active);
```

**Learning Objectives:**
- Dynamic DOM updates
- Template rendering
- State synchronization

**Extension:** Add virtual scrolling for large lists.

---

### Assignment I9: Building a Modal
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 40 mins

**Problem Statement:**
Create a reusable modal component.

**Requirements:**
```javascript
class Modal {
  constructor(options) { }
  // options: { title, content, closable, backdrop, animation }
  open() { }
  close() { }
  setContent(html) { }
  setTitle(title) { }
  on(event, handler) { }  // 'open', 'close', 'beforeClose'
  static confirm(message) { }  // Returns Promise<boolean>
  static alert(message) { }
  static prompt(message, defaultValue) { }
}
```

**Test Cases:**
```javascript
const modal = new Modal({ title: 'Confirm', closable: true });
modal.open();
modal.on('close', () => console.log('Modal closed'));

const confirmed = await Modal.confirm('Are you sure?');
```

**Learning Objectives:**
- Build reusable components
- Handle component lifecycle
- Implement keyboard accessibility

**Extension:** Add nested modal support.

---

### Assignment I10: Building Tabs
**Difficulty:** ⭐⭐ (2/5) | **Time:** 35 mins

**Problem Statement:**
Create a tabs component.

**Requirements:**
```javascript
class Tabs {
  constructor(container, options) { }
  // options: { activeIndex, animated }
  activate(index) { }
  next() { }
  prev() { }
  addTab(label, content) { }
  removeTab(index) { }
  on(event, handler) { }  // 'change', 'beforeChange'
  getActiveTab() { }
}
```

**HTML Structure:**
```html
<div class="tabs">
  <div class="tab-headers">
    <button class="tab-btn active">Tab 1</button>
    <button class="tab-btn">Tab 2</button>
  </div>
  <div class="tab-panels">
    <div class="tab-panel active">Content 1</div>
    <div class="tab-panel">Content 2</div>
  </div>
</div>
```

**Learning Objectives:**
- Manage active states
- Keyboard navigation
- CSS transitions

**Extension:** Add lazy loading for tab content.

---

### Assignment I11: Building an Accordion
**Difficulty:** ⭐⭐ (2/5) | **Time:** 35 mins

**Problem Statement:**
Create an accordion component.

**Requirements:**
```javascript
class Accordion {
  constructor(container, options) { }
  // options: { multiple, animated, defaultOpen }
  toggle(index) { }
  open(index) { }
  close(index) { }
  openAll() { }
  closeAll() { }
  addSection(header, content) { }
  on(event, handler) { }
}
```

**Learning Objectives:**
- Toggle visibility smoothly
- Handle multiple vs single open
- Animate height changes

**Extension:** Add nested accordions.

---

### Assignment I12: Image Carousel
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 45 mins

**Problem Statement:**
Create an image carousel/slider.

**Requirements:**
```javascript
class Carousel {
  constructor(container, options) { }
  // options: { autoplay, interval, pauseOnHover, dots, arrows }
  next() { }
  prev() { }
  goTo(index) { }
  play() { }
  pause() { }
  addSlide(content) { }
  removeSlide(index) { }
  on(event, handler) { } // 'change', 'autoplayStart', 'autoplayStop'
}
```

**Learning Objectives:**
- CSS transforms for sliding
- Autoplay with intervals
- Touch/swipe support concept

**Extension:** Add infinite loop and lazy loading.

---

### Assignment I13: Tooltip Component
**Difficulty:** ⭐⭐ (2/5) | **Time:** 30 mins

**Problem Statement:**
Create a tooltip system.

**Requirements:**
```javascript
class Tooltip {
  constructor(options) { }
  // options: { position, trigger, delay, animation }
  attach(element, content) { }
  detach(element) { }
  show(element) { }
  hide(element) { }
  updateContent(element, content) { }
  static init(selector, options) { } // Auto-attach to elements
}
```

**Learning Objectives:**
- Position elements dynamically
- Handle hover/focus events
- Viewport boundary detection

**Extension:** Add HTML content and interactive tooltips.

---

### Assignment I14: Dropdown Menu
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 40 mins

**Problem Statement:**
Create a dropdown menu component.

**Requirements:**
```javascript
class Dropdown {
  constructor(trigger, menu, options) { }
  // options: { position, closeOnClick, closeOnOutside }
  open() { }
  close() { }
  toggle() { }
  setItems(items) { }
  on(event, handler) { } // 'select', 'open', 'close'
}
```

**Learning Objectives:**
- Handle outside clicks
- Position dropdown correctly
- Keyboard navigation (arrows, enter, escape)

**Extension:** Add nested dropdown support.

---

### Assignment I15: Notification System
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 40 mins

**Problem Statement:**
Create a toast notification system.

**Requirements:**
```javascript
class NotificationManager {
  static success(message, options) { }
  static error(message, options) { }
  static warning(message, options) { }
  static info(message, options) { }
  // options: { duration, position, dismissible, action }
  static clear() { }
  static clearAll() { }
}
```

**Learning Objectives:**
- Stack multiple notifications
- Auto-dismiss with timers
- Animate enter/exit

**Extension:** Add progress bar and actions.

---

## Module 2: Events and Event Handling

### Assignment I16: Event Basics
**Difficulty:** ⭐⭐ (2/5) | **Time:** 25 mins

**Problem Statement:**
Create an event utility library.

**Requirements:**
```javascript
const EventUtils = {
  on(element, event, handler, options) { },
  off(element, event, handler) { },
  once(element, event, handler) { },
  trigger(element, event, detail) { },
  delegate(parent, event, selector, handler) { },
  ready(callback) { },               // DOMContentLoaded
  loaded(callback) { },              // window.load
};
```

**Test Cases:**
```javascript
EventUtils.on(button, 'click', handleClick);
EventUtils.delegate(list, 'click', 'li', handleItemClick);
EventUtils.once(form, 'submit', handleFirstSubmit);
```

**Learning Objectives:**
- Add/remove event listeners
- Use event delegation
- Understand event options

**Extension:** Add event namespacing.

---

### Assignment I17: Event Object Deep Dive
**Difficulty:** ⭐⭐ (2/5) | **Time:** 25 mins

**Problem Statement:**
Create an event inspector utility.

**Requirements:**
```javascript
function inspectEvent(event) {
  return {
    type: event.type,
    target: event.target,
    currentTarget: event.currentTarget,
    phase: event.eventPhase,
    bubbles: event.bubbles,
    cancelable: event.cancelable,
    timestamp: event.timeStamp,
    // Mouse events
    position: { x: event.clientX, y: event.clientY },
    // Keyboard events
    key: event.key,
    modifiers: { ctrl, alt, shift, meta }
  };
}
```

**Learning Objectives:**
- Understand event properties
- Differentiate target vs currentTarget
- Handle different event types

**Extension:** Create an event logger/debugger.

---

### Assignment I18: Bubbling and Capturing
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 30 mins

**Problem Statement:**
Demonstrate and utilize event propagation.

**Requirements:**
Create a visualization of event bubbling/capturing:
```javascript
class EventPropagationDemo {
  constructor(container) { }
  setupListeners() { }           // Add to all nested elements
  logPropagation(event, phase) { }
  stopAtElement(selector) { }    // Stop propagation here
  captureOnly() { }              // Use capture phase
}
```

**Learning Objectives:**
- Understand event phases
- Use stopPropagation correctly
- Implement capture phase

**Extension:** Visualize propagation with animation.

---

### Assignment I19: Event Delegation
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 35 mins

**Problem Statement:**
Implement advanced event delegation.

**Requirements:**
```javascript
class DelegatedEvents {
  constructor(root) { }
  on(selector, event, handler) { }
  off(selector, event) { }
  // Handle dynamically added elements
  // Support multiple events per selector
  // Support namespaced events
}
```

**Test Cases:**
```javascript
const events = new DelegatedEvents(document.body);
events.on('.card', 'click', handleCardClick);
events.on('.card .btn', 'click', handleButtonClick);
// Works even for cards added later
```

**Learning Objectives:**
- Efficient event handling
- Handle dynamic content
- Optimize memory usage

**Extension:** Add event priority/ordering.

---

### Assignment I20: Form Events
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 40 mins

**Problem Statement:**
Create a comprehensive form handler.

**Requirements:**
```javascript
class FormHandler {
  constructor(form, options) { }
  // options: { validateOnBlur, validateOnInput, submitHandler }
  validate() { }
  getValues() { }                // All form data as object
  setValues(data) { }
  reset() { }
  serialize() { }                // URL encoded string
  serializeJSON() { }
  onChange(handler) { }
  onSubmit(handler) { }
  disable() { }
  enable() { }
}
```

**Learning Objectives:**
- Handle form submission
- Serialize form data
- Validate on various events

**Extension:** Add file upload handling.

---

### Assignment I21: Keyboard Events
**Difficulty:** ⭐⭐ (2/5) | **Time:** 30 mins

**Problem Statement:**
Create a keyboard shortcut manager.

**Requirements:**
```javascript
class KeyboardShortcuts {
  constructor() { }
  bind(combo, handler) { }       // 'ctrl+s', 'alt+shift+n'
  unbind(combo) { }
  enable() { }
  disable() { }
  pause() { }                    // Temporarily disable
  resume() { }
  list() { }                     // Return all shortcuts
}
```

**Test Cases:**
```javascript
const shortcuts = new KeyboardShortcuts();
shortcuts.bind('ctrl+s', (e) => {
  e.preventDefault();
  saveDocument();
});
shortcuts.bind('escape', closeModal);
```

**Learning Objectives:**
- Handle keyboard combinations
- Prevent default behaviors
- Manage shortcut conflicts

**Extension:** Add scope-based shortcuts (editor, modal, etc.).

---

### Assignment I22: Mouse Events
**Difficulty:** ⭐⭐ (2/5) | **Time:** 30 mins

**Problem Statement:**
Create a mouse interaction tracker.

**Requirements:**
```javascript
class MouseTracker {
  constructor(element) { }
  onMove(handler) { }            // Throttled
  onClick(handler) { }
  onDoubleClick(handler) { }
  onRightClick(handler) { }
  onDragStart(handler) { }
  onDrag(handler) { }
  onDragEnd(handler) { }
  getPosition() { }              // Current position
  isInElement(element) { }
}
```

**Learning Objectives:**
- Track mouse position
- Differentiate click types
- Implement custom drag

**Extension:** Add gesture recognition (swipe, pinch concept).

---

### Assignment I23: Custom Events
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 35 mins

**Problem Statement:**
Create a custom event system.

**Requirements:**
```javascript
class EventEmitter {
  on(event, handler) { }
  off(event, handler) { }
  once(event, handler) { }
  emit(event, data) { }
  removeAllListeners(event) { }
  listenerCount(event) { }
  eventNames() { }
}

// DOM custom events:
function dispatchCustomEvent(element, name, detail) { }
```

**Test Cases:**
```javascript
const emitter = new EventEmitter();
emitter.on('data', (d) => console.log(d));
emitter.emit('data', { value: 42 }); // Logs { value: 42 }
```

**Learning Objectives:**
- Implement pub/sub pattern
- Create CustomEvents for DOM
- Decouple components

**Extension:** Add event wildcards and namespaces.

---

### Assignment I24: Prevent Default & Stop Propagation
**Difficulty:** ⭐⭐ (2/5) | **Time:** 25 mins

**Problem Statement:**
Create examples demonstrating when to use each.

**Requirements:**
```javascript
// Implement these scenarios:
class PreventDefaultExamples {
  preventFormSubmit() { }        // Custom AJAX submission
  preventLinkNavigation() { }    // SPA routing
  preventContextMenu() { }       // Custom right-click menu
  preventDrag() { }             // Disable native drag
  allowOnlyNumbers(input) { }   // Filter keystrokes
}

class StopPropagationExamples {
  modalBackdrop() { }           // Click inside shouldn't close
  nestedButtons() { }           // Parent shouldn't trigger
  editableTable() { }           // Cell edit vs row select
}
```

**Learning Objectives:**
- Know when to prevent default
- Know when to stop propagation
- Avoid common anti-patterns

**Extension:** Create debugging tools for event issues.

---

### Assignment I25: Touch Events
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 40 mins

**Problem Statement:**
Create a touch gesture handler.

**Requirements:**
```javascript
class TouchGestures {
  constructor(element) { }
  onTap(handler) { }
  onDoubleTap(handler) { }
  onLongPress(handler, duration) { }
  onSwipe(handler) { }           // direction: up, down, left, right
  onPinch(handler) { }           // scale factor
  onRotate(handler) { }          // angle
  onPan(handler) { }             // x, y delta
}
```

**Learning Objectives:**
- Handle touch events
- Calculate gestures from touches
- Support multi-touch

**Extension:** Add momentum scrolling.

---

### Assignment I26: Scroll Events
**Difficulty:** ⭐⭐ (2/5) | **Time:** 30 mins

**Problem Statement:**
Create scroll-related utilities.

**Requirements:**
```javascript
class ScrollUtils {
  static getPosition() { }        // Current scroll position
  static scrollTo(options) { }    // Smooth scroll
  static scrollToElement(el) { }
  static onScroll(handler) { }    // Throttled
  static onScrollEnd(handler) { }
  static getDirection() { }       // up or down
  static isAtBottom() { }
  static isAtTop() { }
  static getScrollPercent() { }
}
```

**Learning Objectives:**
- Track scroll position
- Implement smooth scrolling
- Optimize scroll handlers

**Extension:** Add parallax scrolling helpers.

---

### Assignment I27: Resize Events
**Difficulty:** ⭐⭐ (2/5) | **Time:** 25 mins

**Problem Statement:**
Create responsive resize handlers.

**Requirements:**
```javascript
class ResizeHandler {
  constructor(options) { }
  // options: { debounceMs, breakpoints }
  onResize(handler) { }
  onBreakpointChange(handler) { }
  getCurrentBreakpoint() { }
  isBreakpoint(name) { }
  isMobile() { }
  isTablet() { }
  isDesktop() { }
}
```

**Learning Objectives:**
- Handle window resize efficiently
- Implement breakpoint detection
- Debounce resize handlers

**Extension:** Add element resize observation (ResizeObserver).

---

### Assignment I28: Focus Events
**Difficulty:** ⭐⭐ (2/5) | **Time:** 25 mins

**Problem Statement:**
Create a focus management system.

**Requirements:**
```javascript
class FocusManager {
  static trap(container) { }      // Tab stays within container
  static release() { }
  static getFirstFocusable(container) { }
  static getLastFocusable(container) { }
  static getAllFocusable(container) { }
  static focusFirst(container) { }
  static focusLast(container) { }
  static saveFocus() { }
  static restoreFocus() { }
}
```

**Learning Objectives:**
- Manage keyboard focus
- Implement focus traps
- Handle modal accessibility

**Extension:** Add focus ring visibility management.

---

### Assignment I29: Clipboard Events
**Difficulty:** ⭐⭐ (2/5) | **Time:** 25 mins

**Problem Statement:**
Create a clipboard utility.

**Requirements:**
```javascript
class ClipboardManager {
  static async copy(text) { }     // Modern Clipboard API
  static async paste() { }
  static async copyRichText(html) { }
  static onCopy(handler) { }
  static onPaste(handler) { }
  static onCut(handler) { }
  static copyToClipboard(element) { } // Copy element contents
}
```

**Learning Objectives:**
- Use Clipboard API
- Handle clipboard events
- Request permissions

**Extension:** Add image clipboard support.

---

### Assignment I30: Drag and Drop API
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 45 mins

**Problem Statement:**
Create a drag and drop system.

**Requirements:**
```javascript
class DragDropManager {
  constructor(options) { }
  makeDraggable(element, options) { }
  makeDropZone(element, options) { }
  // options: { data, type, onDragStart, onDragEnd }
  // dropOptions: { accept, onDrop, onDragOver, onDragEnter, onDragLeave }
  enableSorting(container) { }    // Reorderable list
}
```

**Learning Objectives:**
- Implement HTML5 drag and drop
- Transfer data between elements
- Create sortable lists

**Extension:** Add touch support for drag and drop.

---

### Assignment I31: Form Validation
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 45 mins

**Problem Statement:**
Create a comprehensive form validation system.

**Requirements:**
```javascript
class FormValidator {
  constructor(form, rules) { }
  addRule(field, rule) { }
  removeRule(field, ruleName) { }
  validate() { }                  // Returns { valid, errors }
  validateField(field) { }
  showErrors() { }
  clearErrors() { }
  onValidate(handler) { }
  
  // Built-in rules:
  static rules = {
    required, email, minLength, maxLength, pattern,
    min, max, equalTo, custom
  };
}
```

**Test Cases:**
```javascript
const validator = new FormValidator(form, {
  email: [
    { rule: 'required', message: 'Email is required' },
    { rule: 'email', message: 'Invalid email' }
  ],
  password: [
    { rule: 'required' },
    { rule: 'minLength', value: 8 }
  ],
  confirmPassword: [
    { rule: 'equalTo', value: 'password' }
  ]
});
```

**Learning Objectives:**
- Implement validation rules
- Show inline errors
- Handle async validation

**Extension:** Add conditional validation rules.

---

### Assignment I32: Infinite Scroll
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 40 mins

**Problem Statement:**
Implement infinite scroll functionality.

**Requirements:**
```javascript
class InfiniteScroll {
  constructor(container, options) { }
  // options: { threshold, loadMore, hasMore }
  enable() { }
  disable() { }
  reset() { }
  setLoader(element) { }
  on(event, handler) { }  // 'load', 'end', 'error'
}
```

**Learning Objectives:**
- Use IntersectionObserver
- Load content on scroll
- Handle loading states

**Extension:** Add virtual scrolling for performance.

---

### Assignment I33: Lazy Loading Images
**Difficulty:** ⭐⭐ (2/5) | **Time:** 30 mins

**Problem Statement:**
Implement lazy loading for images.

**Requirements:**
```javascript
class LazyLoader {
  constructor(options) { }
  // options: { root, rootMargin, threshold, placeholder }
  observe(element) { }
  unobserve(element) { }
  observeAll(selector) { }
  forceLoad(element) { }
}
```

**Usage:**
```html
<img data-src="image.jpg" data-srcset="..." class="lazy">
```

**Learning Objectives:**
- Use IntersectionObserver
- Handle image loading states
- Improve page performance

**Extension:** Add blur-up effect during loading.

---

### Assignment I34: Debounce and Throttle
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 35 mins

**Problem Statement:**
Implement debounce and throttle utilities.

**Requirements:**
```javascript
function debounce(fn, delay, options) { }
// options: { leading, trailing }

function throttle(fn, limit, options) { }
// options: { leading, trailing }

// Usage examples:
const debouncedSearch = debounce(search, 300);
const throttledScroll = throttle(handleScroll, 100);
```

**Test Cases:**
```javascript
const debounced = debounce(fn, 100);
debounced(); debounced(); debounced();  // Called once after 100ms

const throttled = throttle(fn, 100);
// Rapid calls result in one call per 100ms
```

**Learning Objectives:**
- Understand debounce vs throttle
- Implement with options
- Apply to real scenarios

**Extension:** Add cancel and flush methods.

---

### Assignment I35: Event Debugging Tools
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 40 mins

**Problem Statement:**
Create debugging tools for events.

**Requirements:**
```javascript
class EventDebugger {
  static logAllEvents(element, filter) { }
  static monitorEvent(element, event) { }
  static countEvents(element, event, duration) { }
  static measureEventTime(element, events) { } // Time between events
  static visualizeClicks(element) { }  // Show click positions
  static highlightListeners(element) { }
}
```

**Learning Objectives:**
- Debug event issues
- Measure event performance
- Visualize event flow

**Extension:** Create browser extension for event debugging.

---

## Module 3: Asynchronous JavaScript

### Assignment I36: setTimeout and setInterval
**Difficulty:** ⭐⭐ (2/5) | **Time:** 25 mins

**Problem Statement:**
Create timer utilities.

**Requirements:**
```javascript
class Timer {
  static delay(ms) { }             // Returns Promise
  static interval(fn, ms) { }      // Returns controller
  static timeout(fn, ms) { }       // Returns controller
  // controller: { start, stop, pause, resume, isRunning }
}

class CountdownTimer {
  constructor(seconds, onTick, onComplete) { }
  start() { }
  pause() { }
  resume() { }
  reset() { }
  getRemaining() { }
}
```

**Test Cases:**
```javascript
await Timer.delay(1000); // Waits 1 second
const interval = Timer.interval(() => console.log('tick'), 1000);
interval.stop(); // Stops the interval
```

**Learning Objectives:**
- Use setTimeout/setInterval
- Create controllable timers
- Handle cleanup

**Extension:** Add drift correction for accurate intervals.

---

### Assignment I37: Callbacks Deep Dive
**Difficulty:** ⭐⭐ (2/5) | **Time:** 25 mins

**Problem Statement:**
Work with callback patterns.

**Requirements:**
```javascript
// Implement callback-based functions:
function readFileAsync(path, callback) { }  // Simulated
function fetchDataAsync(url, callback) { }  // Simulated
function processInSequence(tasks, callback) { }
function processInParallel(tasks, callback) { }

// Error-first callback pattern:
function doAsync(callback) {
  // callback(error, result)
}
```

**Test Cases:**
```javascript
processInSequence([
  cb => setTimeout(() => cb(null, 1), 100),
  cb => setTimeout(() => cb(null, 2), 100),
], (err, results) => console.log(results)); // [1, 2]
```

**Learning Objectives:**
- Understand error-first callbacks
- Sequential vs parallel execution
- Handle callback errors

**Extension:** Create a callback-to-promise converter.

---

### Assignment I38: Callback Hell
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 35 mins

**Problem Statement:**
Identify and refactor callback hell.

**Requirements:**
```javascript
// Refactor this callback hell:
function fetchUserData(userId, callback) {
  getUser(userId, (err, user) => {
    if (err) return callback(err);
    getProfile(user.profileId, (err, profile) => {
      if (err) return callback(err);
      getPosts(user.id, (err, posts) => {
        if (err) return callback(err);
        getComments(posts[0].id, (err, comments) => {
          if (err) return callback(err);
          callback(null, { user, profile, posts, comments });
        });
      });
    });
  });
}

// Solution approaches:
// 1. Named functions
// 2. Modularization
// 3. Control flow libraries
// 4. Promises
```

**Learning Objectives:**
- Recognize callback hell
- Apply refactoring patterns
- Improve code readability

**Extension:** Create an async flow control library.

---

### Assignment I39: Promise Basics
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 30 mins

**Problem Statement:**
Master Promise creation and usage.

**Requirements:**
```javascript
// Create these Promise-based utilities:
function wait(ms) { }                    // Resolve after ms
function waitRandom(min, max) { }        // Random delay
function timeout(promise, ms) { }        // Reject if too slow
function retry(fn, attempts, delay) { }  // Retry failed promises
function promisify(fn) { }               // Convert callback to promise
```

**Test Cases:**
```javascript
await wait(1000); // Waits 1 second

const result = await timeout(
  fetch('/api/slow'),
  5000
); // Throws if > 5 seconds

const readFile = promisify(fs.readFile);
const data = await readFile('file.txt');
```

**Learning Objectives:**
- Create Promises correctly
- Handle Promise states
- Convert callbacks to Promises

**Extension:** Implement a lazy Promise.

---

### Assignment I40: Promise Chaining
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 30 mins

**Problem Statement:**
Master Promise chaining patterns.

**Requirements:**
```javascript
// Refactor callback hell example to promises:
function fetchUserDataPromise(userId) {
  return getUser(userId)
    .then(user => ...)
    .then(...)
}

// Create chainable API:
class ChainableRequest {
  constructor(url) { }
  setHeader(key, value) { }
  setBody(body) { }
  get() { }
  post() { }
  then(onFulfill, onReject) { }
}
```

**Test Cases:**
```javascript
const result = await fetchUserDataPromise(1);
// { user, profile, posts, comments }

const data = await new ChainableRequest('/api/users')
  .setHeader('Auth', 'token')
  .setBody({ name: 'John' })
  .post();
```

**Learning Objectives:**
- Chain promises effectively
- Pass data through chains
- Create thenable objects

**Extension:** Add request/response interceptors.

---

### Assignment I41: Promise Error Handling
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 35 mins

**Problem Statement:**
Master Promise error handling.

**Requirements:**
```javascript
// Demonstrate error handling patterns:
class PromiseErrorPatterns {
  static catchInChain() { }         // .catch in middle of chain
  static catchAtEnd() { }           // .catch at end
  static catchAndRecover() { }      // Return default value
  static catchAndRethrow() { }      // Transform error
  static finallyCleanup() { }       // Use .finally
  static handleUnhandled() { }      // Global handler
}

// Create robust error handling:
async function robustFetch(url, options) {
  // Handle network errors
  // Handle HTTP errors
  // Handle timeout
  // Handle parse errors
  // Provide meaningful messages
}
```

**Learning Objectives:**
- Handle errors in chains
- Recover from errors
- Clean up with finally

**Extension:** Create error classification system.

---

### Assignment I42: Promise Static Methods
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 35 mins

**Problem Statement:**
Implement Promise static methods from scratch.

**Requirements:**
```javascript
const MyPromise = {
  all(promises) { },           // All must succeed
  allSettled(promises) { },    // Wait for all, regardless
  race(promises) { },          // First to settle
  any(promises) { },           // First to succeed
  resolve(value) { },
  reject(reason) { },
};
```

**Test Cases:**
```javascript
const results = await MyPromise.all([
  fetch('/api/1'),
  fetch('/api/2'),
  fetch('/api/3')
]);

const first = await MyPromise.race([
  fetch('/api/fast'),
  MyPromise.delay(1000).then(() => 'timeout')
]);
```

**Learning Objectives:**
- Understand all Promise methods
- Know when to use each
- Handle mixed results

**Extension:** Implement Promise.map with concurrency limit.

---

### Assignment I43: Async/Await Basics
**Difficulty:** ⭐⭐ (2/5) | **Time:** 25 mins

**Problem Statement:**
Convert Promises to async/await.

**Requirements:**
```javascript
// Convert to async/await:
function fetchUserDataPromise(userId) {
  return getUser(userId)
    .then(user => getProfile(user.profileId).then(profile => ({user, profile})))
    .then(({user, profile}) => getPosts(user.id).then(posts => ({user, profile, posts})))
    .then(data => getComments(data.posts[0].id).then(comments => ({...data, comments})));
}

// Result:
async function fetchUserData(userId) {
  // Clean, readable version
}
```

**Learning Objectives:**
- Use async/await syntax
- Handle sequential operations
- Improve readability

**Extension:** Measure performance vs Promise chains.

---

### Assignment I44: Async Error Handling
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 30 mins

**Problem Statement:**
Master try/catch with async/await.

**Requirements:**
```javascript
// Implement error handling patterns:
async function withErrorHandling() {
  // Try-catch-finally
  // Handling multiple await
  // Error recovery
  // Custom error types
}

// Create error utility:
async function tryCatch(fn) {
  // Return [error, result] tuple
}

// Usage:
const [error, user] = await tryCatch(() => fetchUser(id));
if (error) handleError(error);
```

**Learning Objectives:**
- Handle async errors properly
- Create error utilities
- Avoid unhandled rejections

**Extension:** Create async error boundary pattern.

---

### Assignment I45: Concurrent Async Operations
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 35 mins

**Problem Statement:**
Handle multiple async operations efficiently.

**Requirements:**
```javascript
class AsyncOps {
  // Run in parallel (Promise.all style)
  static async parallel(tasks) { }
  
  // Run in series
  static async series(tasks) { }
  
  // Run with concurrency limit
  static async pool(tasks, concurrency) { }
  
  // Race with timeout
  static async raceWithTimeout(task, ms) { }
  
  // All settled with async/await
  static async allSettled(tasks) { }
}
```

**Test Cases:**
```javascript
const results = await AsyncOps.pool([
  () => fetch('/1'),
  () => fetch('/2'),
  () => fetch('/3'),
  () => fetch('/4'),
  () => fetch('/5')
], 2); // Only 2 concurrent
```

**Learning Objectives:**
- Control concurrency
- Optimize async operations
- Handle partial failures

**Extension:** Add progress tracking for pool operations.

---

### Assignment I46: Fetch API
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 40 mins

**Problem Statement:**
Create a complete HTTP client using Fetch.

**Requirements:**
```javascript
class HttpClient {
  constructor(baseUrl, options) { }
  
  async get(path, options) { }
  async post(path, body, options) { }
  async put(path, body, options) { }
  async patch(path, body, options) { }
  async delete(path, options) { }
  
  setHeader(key, value) { }
  setBearerToken(token) { }
  setTimeout(ms) { }
  
  addRequestInterceptor(fn) { }
  addResponseInterceptor(fn) { }
}
```

**Test Cases:**
```javascript
const api = new HttpClient('https://api.example.com', {
  headers: { 'Content-Type': 'application/json' }
});

api.setBearerToken('my-token');
const users = await api.get('/users');
await api.post('/users', { name: 'John' });
```

**Learning Objectives:**
- Master Fetch API
- Handle all HTTP methods
- Build reusable client

**Extension:** Add request caching and deduplication.

---

### Assignment I47: API Error Handling
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 35 mins

**Problem Statement:**
Handle API errors comprehensively.

**Requirements:**
```javascript
class ApiError extends Error {
  constructor(response, body) { }
  // Properties: status, statusText, body, isTimeout, isNetwork
}

async function fetchWithErrors(url, options) {
  // Handle network errors
  // Handle HTTP status errors
  // Handle JSON parse errors
  // Handle timeout
  // Provide retry capability
}

function categorizeError(error) {
  // 'network' | 'timeout' | 'auth' | 'validation' | 'server' | 'unknown'
}
```

**Learning Objectives:**
- Create custom error classes
- Categorize API errors
- Implement retry logic

**Extension:** Add error reporting to logging service.

---

### Assignment I48: Working with JSON APIs
**Difficulty:** ⭐⭐ (2/5) | **Time:** 30 mins

**Problem Statement:**
Build utilities for JSON API interaction.

**Requirements:**
```javascript
class JsonApi {
  constructor(baseUrl) { }
  
  async getResource(type, id) { }
  async listResources(type, filters) { }
  async createResource(type, data) { }
  async updateResource(type, id, data) { }
  async deleteResource(type, id) { }
  
  // Handle relationships
  async getRelated(type, id, relationship) { }
  
  // Handle pagination
  async paginate(type, options) { }
}
```

**Test Cases:**
```javascript
const api = new JsonApi('https://jsonplaceholder.typicode.com');
const users = await api.listResources('users');
const user = await api.getResource('users', 1);
const posts = await api.getRelated('users', 1, 'posts');
```

**Learning Objectives:**
- Work with REST APIs
- Handle pagination
- Follow API conventions

**Extension:** Add GraphQL support.

---

### Assignment I49: Request Cancellation
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 35 mins

**Problem Statement:**
Implement request cancellation using AbortController.

**Requirements:**
```javascript
class CancellableFetch {
  constructor() { }
  
  fetch(url, options) { }
  cancel(reason) { }
  cancelAll() { }
  onCancel(handler) { }
}

// Hook pattern for React-like usage:
function useFetch(url) {
  // Returns { data, loading, error, cancel, refetch }
  // Cancels on unmount/url change
}
```

**Test Cases:**
```javascript
const cancellable = new CancellableFetch();
const promise = cancellable.fetch('/api/slow');

setTimeout(() => cancellable.cancel('User cancelled'), 1000);

try {
  await promise;
} catch (e) {
  console.log(e.name); // 'AbortError'
}
```

**Learning Objectives:**
- Use AbortController
- Cancel ongoing requests
- Handle cancellation gracefully

**Extension:** Add request deduplication.

---

### Assignment I50: Real-time Updates
**Difficulty:** ⭐⭐⭐⭐ (4/5) | **Time:** 45 mins

**Problem Statement:**
Implement real-time update patterns.

**Requirements:**
```javascript
class RealTimeUpdater {
  // Polling approach
  static poll(fn, interval, options) { }
  
  // Long polling
  static longPoll(url, onMessage, options) { }
  
  // Server-Sent Events
  static sse(url, onMessage, options) { }
}

class PollingService {
  constructor(fetchFn, interval) { }
  start() { }
  stop() { }
  pause() { }
  resume() { }
  onData(handler) { }
  onError(handler) { }
}
```

**Learning Objectives:**
- Implement polling patterns
- Handle SSE connections
- Manage connection lifecycle

**Extension:** Add WebSocket wrapper.

---

## Module 4: Web Storage and Intermediate Projects

### Assignment I51: Local Storage
**Difficulty:** ⭐⭐ (2/5) | **Time:** 25 mins

**Problem Statement:**
Create a localStorage wrapper.

**Requirements:**
```javascript
class LocalStore {
  static get(key, defaultValue) { }
  static set(key, value) { }
  static remove(key) { }
  static clear() { }
  static has(key) { }
  static keys() { }
  static size() { }
  
  // Auto JSON serialization
  static getObject(key) { }
  static setObject(key, value) { }
  
  // Expiring items
  static setWithExpiry(key, value, ttl) { }
  static getWithExpiry(key) { }
}
```

**Learning Objectives:**
- Use localStorage API
- Handle serialization
- Implement expiry mechanism

**Extension:** Add storage events for cross-tab sync.

---

### Assignment I52: Session Storage
**Difficulty:** ⭐⭐ (2/5) | **Time:** 20 mins

**Problem Statement:**
Create a sessionStorage utility.

**Requirements:**
```javascript
class SessionStore {
  static get(key) { }
  static set(key, value) { }
  static remove(key) { }
  static clear() { }
  
  // Session-specific features
  static flash(key, value) { }   // Auto-remove after first read
  static increment(key) { }
  static decrement(key) { }
}
```

**Learning Objectives:**
- Understand session scope
- Difference from localStorage
- Flash message pattern

**Extension:** Add session timeout tracking.

---

### Assignment I53: Interactive Todo App
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 60 mins

**Problem Statement:**
Build a full-featured todo app with DOM and storage.

**Requirements:**
```javascript
class TodoApp {
  constructor(container) { }
  
  // CRUD
  addTodo(text, category) { }
  removeTodo(id) { }
  toggleTodo(id) { }
  editTodo(id, text) { }
  
  // Filtering
  filterBy(status) { }        // 'all' | 'active' | 'completed'
  filterByCategory(category) { }
  searchTodos(query) { }
  
  // Bulk actions
  clearCompleted() { }
  markAllComplete() { }
  
  // Persistence
  save() { }
  load() { }
  
  // Stats
  getStats() { }
}
```

**Features:**
- Add/edit/delete todos
- Mark complete/incomplete
- Filter by status
- Search todos
- Categories/tags
- Persist to localStorage
- Undo/redo operations
- Drag to reorder

**Learning Objectives:**
- Combine DOM manipulation with events
- Implement CRUD operations
- Persist application state

**Extension:** Add due dates and reminders.

---

### Assignment I54: Quiz Application
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 60 mins

**Problem Statement:**
Build an interactive quiz application.

**Requirements:**
```javascript
class QuizApp {
  constructor(container, questions) { }
  
  start() { }
  nextQuestion() { }
  prevQuestion() { }
  submitAnswer(answer) { }
  finish() { }
  
  getProgress() { }
  getScore() { }
  getResults() { }
  
  // Timer
  startTimer(seconds) { }
  pauseTimer() { }
  
  // Shuffle
  shuffleQuestions() { }
  shuffleAnswers() { }
}
```

**Features:**
- Multiple question types (single, multiple, true/false)
- Timer countdown
- Progress indicator
- Score calculation
- Review wrong answers
- High score tracking

**Learning Objectives:**
- Dynamic content updates
- State management
- Timer implementation

**Extension:** Add question categories and difficulty levels.

---

### Assignment I55: Stopwatch/Timer App
**Difficulty:** ⭐⭐ (2/5) | **Time:** 40 mins

**Problem Statement:**
Build a stopwatch and countdown timer.

**Requirements:**
```javascript
class StopwatchTimer {
  constructor(container) { }
  
  // Stopwatch mode
  startStopwatch() { }
  stopStopwatch() { }
  resetStopwatch() { }
  lap() { }
  getLaps() { }
  
  // Timer mode
  setTimer(seconds) { }
  startTimer() { }
  pauseTimer() { }
  resetTimer() { }
  
  // Display
  formatTime(ms) { }
  updateDisplay() { }
}
```

**Features:**
- Start/stop/reset
- Lap times
- Countdown with alarm
- Multiple timers
- Persist running timers

**Learning Objectives:**
- Precise timing
- UI updates at intervals
- Handle background tabs

**Extension:** Add Pomodoro timer mode.

---

### Assignment I56: Weather Dashboard
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 60 mins

**Problem Statement:**
Build a weather dashboard using public API.

**Requirements:**
```javascript
class WeatherDashboard {
  constructor(container, apiKey) { }
  
  async searchCity(query) { }
  async getCurrentWeather(city) { }
  async getForecast(city, days) { }
  
  async getByLocation() { }      // Use geolocation
  
  addToFavorites(city) { }
  removeFromFavorites(city) { }
  getFavorites() { }
  
  renderCurrent(data) { }
  renderForecast(data) { }
}
```

**Features:**
- Search by city
- Current weather display
- 5-day forecast
- Geolocation support
- Favorite cities
- Unit conversion (C/F)
- Weather icons

**Learning Objectives:**
- Work with real APIs
- Handle geolocation
- Display complex data

**Extension:** Add weather alerts and maps.

---

### Assignment I57: Image Gallery with Filters
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 50 mins

**Problem Statement:**
Build a filterable image gallery.

**Requirements:**
```javascript
class ImageGallery {
  constructor(container, images) { }
  
  render() { }
  filterByCategory(category) { }
  sortBy(field, order) { }
  search(query) { }
  
  openLightbox(index) { }
  closeLightbox() { }
  lightboxNext() { }
  lightboxPrev() { }
  
  lazyLoadImages() { }
}
```

**Features:**
- Grid layout
- Category filtering
- Search by title/tags
- Lightbox viewer
- Keyboard navigation
- Lazy loading
- Loading states

**Learning Objectives:**
- Dynamic filtering
- Lightbox implementation
- Lazy loading

**Extension:** Add image upload and slideshow.

---

### Assignment I58: Search Autocomplete
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 45 mins

**Problem Statement:**
Build a search autocomplete component.

**Requirements:**
```javascript
class Autocomplete {
  constructor(input, options) { }
  // options: { data, fetchFn, minChars, debounceMs, maxResults }
  
  setData(data) { }
  async fetchSuggestions(query) { }
  
  showSuggestions(suggestions) { }
  hideSuggestions() { }
  
  onSelect(handler) { }
  onInput(handler) { }
  
  // Keyboard navigation
  moveUp() { }
  moveDown() { }
  selectCurrent() { }
}
```

**Features:**
- Debounced input
- API or local data
- Keyboard navigation
- Highlight matching text
- Recent searches
- Loading indicator

**Learning Objectives:**
- Debounce user input
- Handle async suggestions
- Keyboard accessibility

**Extension:** Add fuzzy matching and grouping.

---

### Assignment I59: Pagination Component
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 40 mins

**Problem Statement:**
Build a pagination component.

**Requirements:**
```javascript
class Pagination {
  constructor(container, options) { }
  // options: { totalItems, itemsPerPage, currentPage, maxVisible }
  
  goToPage(page) { }
  nextPage() { }
  prevPage() { }
  firstPage() { }
  lastPage() { }
  
  setTotal(total) { }
  setPerPage(perPage) { }
  
  onChange(handler) { }
  render() { }
  
  getPageItems(items) { }        // Slice for current page
}
```

**Features:**
- Page numbers with ellipsis
- First/last buttons
- Previous/next buttons
- Items per page selector
- Current/total display

**Learning Objectives:**
- Calculate pagination
- Handle edge cases
- Update UI on change

**Extension:** Add URL synchronization.

---

### Assignment I60: Shopping Cart
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 60 mins

**Problem Statement:**
Build a shopping cart with DOM and storage.

**Requirements:**
```javascript
class ShoppingCartUI {
  constructor(container) { }
  
  addItem(product) { }
  removeItem(productId) { }
  updateQuantity(productId, quantity) { }
  
  getCartItems() { }
  getSubtotal() { }
  getTax() { }
  getTotal() { }
  
  applyCoupon(code) { }
  removeCoupon() { }
  
  renderCart() { }
  renderSummary() { }
  
  save() { }
  load() { }
}
```

**Features:**
- Add/remove items
- Quantity controls
- Price calculation
- Coupon codes
- Persist to storage
- Cart icon badge
- Checkout summary

**Learning Objectives:**
- E-commerce logic
- State persistence
- Calculate totals

**Extension:** Add product variants and shipping.

---

### Assignment I61: Data Table
**Difficulty:** ⭐⭐⭐⭐ (4/5) | **Time:** 75 mins

**Problem Statement:**
Build a data table with sorting, filtering, and pagination.

**Requirements:**
```javascript
class DataTable {
  constructor(container, options) { }
  // options: { columns, data, sortable, filterable, paginated }
  
  setData(data) { }
  sort(column, direction) { }
  filter(column, value) { }
  search(query) { }
  
  selectRow(index) { }
  selectAll() { }
  deselectAll() { }
  getSelected() { }
  
  exportCSV() { }
  exportJSON() { }
  
  render() { }
}
```

**Features:**
- Column sorting
- Column filtering
- Global search
- Pagination
- Row selection
- Column resizing
- Export data

**Learning Objectives:**
- Complex data display
- Multiple interactions
- Data manipulation

**Extension:** Add inline editing and virtual scrolling.

---

### Assignment I62: Form Builder
**Difficulty:** ⭐⭐⭐⭐ (4/5) | **Time:** 75 mins

**Problem Statement:**
Build a dynamic form builder.

**Requirements:**
```javascript
class FormBuilder {
  constructor(container) { }
  
  addField(config) { }
  // config: { type, name, label, validation, options }
  
  removeField(name) { }
  updateField(name, config) { }
  moveField(from, to) { }
  
  validate() { }
  getValues() { }
  setValues(data) { }
  reset() { }
  
  exportSchema() { }
  importSchema(schema) { }
  
  render() { }
}
```

**Field Types:**
- text, textarea, number
- select, radio, checkbox
- date, time, datetime
- file, range
- custom

**Learning Objectives:**
- Dynamic form creation
- Validation rules
- Schema management

**Extension:** Add conditional fields and multi-step forms.

---

### Assignment I63: Markdown Previewer
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 50 mins

**Problem Statement:**
Build a live markdown editor with preview.

**Requirements:**
```javascript
class MarkdownEditor {
  constructor(editorContainer, previewContainer) { }
  
  setContent(markdown) { }
  getContent() { }
  getHTML() { }
  
  insertAtCursor(text) { }
  wrapSelection(before, after) { }
  
  // Toolbar actions
  bold() { }
  italic() { }
  link() { }
  image() { }
  heading(level) { }
  list(type) { }
  code() { }
  
  save() { }
  load() { }
}
```

**Features:**
- Live preview
- Toolbar buttons
- Keyboard shortcuts
- Syntax highlighting in preview
- Auto-save

**Learning Objectives:**
- Parse markdown
- Live updates
- Editor shortcuts

**Extension:** Add image upload and export to PDF.

---

### Assignment I64: Expense Tracker
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 60 mins

**Problem Statement:**
Build an expense tracking application.

**Requirements:**
```javascript
class ExpenseTracker {
  constructor(container) { }
  
  addExpense(expense) { }
  editExpense(id, expense) { }
  deleteExpense(id) { }
  
  getExpenses(filters) { }
  getByCategory(category) { }
  getByDateRange(start, end) { }
  
  getStats() { }              // Total, by category, by month
  getTrend(months) { }        // Monthly trends
  
  exportCSV() { }
  importCSV(file) { }
  
  renderList() { }
  renderChart() { }
}
```

**Features:**
- Add/edit/delete expenses
- Categories
- Date filtering
- Statistics/summaries
- Basic charts
- Export data

**Learning Objectives:**
- Financial calculations
- Data visualization basics
- Filter and aggregate data

**Extension:** Add income tracking and budgets.

---

### Assignment I65: Note-Taking App
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 55 mins

**Problem Statement:**
Build a note-taking application.

**Requirements:**
```javascript
class NotesApp {
  constructor(container) { }
  
  createNote(title, content) { }
  updateNote(id, data) { }
  deleteNote(id) { }
  
  getNotes(options) { }
  searchNotes(query) { }
  filterByTag(tag) { }
  
  pinNote(id) { }
  unpinNote(id) { }
  archiveNote(id) { }
  
  addTag(noteId, tag) { }
  removeTag(noteId, tag) { }
  
  exportNote(id) { }
  importNotes(data) { }
}
```

**Features:**
- Create/edit/delete notes
- Rich text editing
- Tags and categories
- Search
- Pin/archive
- Trash with recovery
- Auto-save

**Learning Objectives:**
- Content management
- Rich text basics
- Organization features

**Extension:** Add notebooks and sharing.

---

### Assignment I66: Contact Manager
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 45 mins

**Problem Statement:**
Build a contact management app.

**Requirements:**
```javascript
class ContactManager {
  constructor(container) { }
  
  addContact(contact) { }
  editContact(id, contact) { }
  deleteContact(id) { }
  
  getContacts(options) { }
  searchContacts(query) { }
  filterByGroup(group) { }
  
  addToGroup(contactId, group) { }
  removeFromGroup(contactId, group) { }
  createGroup(name) { }
  
  importContacts(data) { }
  exportContacts(format) { }       // vCard, CSV, JSON
  
  renderList() { }
  renderContact(id) { }
}
```

**Features:**
- Contact CRUD
- Groups/categories
- Search and filter
- Avatar support
- Import/export
- Alphabetical index

**Learning Objectives:**
- Contact data handling
- Grouping and filtering
- Multiple display views

**Extension:** Add merge duplicates and favorites.

---

### Assignment I67: Recipe Book
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 55 mins

**Problem Statement:**
Build a recipe management application.

**Requirements:**
```javascript
class RecipeBook {
  constructor(container) { }
  
  addRecipe(recipe) { }
  editRecipe(id, recipe) { }
  deleteRecipe(id) { }
  
  getRecipes(filters) { }
  searchRecipes(query) { }
  filterByCategory(category) { }
  filterByIngredient(ingredient) { }
  
  scaleRecipe(id, servings) { }
  addToFavorites(id) { }
  
  generateShoppingList(recipeIds) { }
  
  renderRecipeCard(recipe) { }
  renderFullRecipe(id) { }
}
```

**Features:**
- Recipe CRUD
- Ingredients with quantities
- Step-by-step instructions
- Categories/tags
- Serving scaler
- Favorites
- Shopping list generator

**Learning Objectives:**
- Complex data structures
- Calculations (scaling)
- Multi-view app

**Extension:** Add meal planning and nutrition info.

---

### Assignment I68: Bookmark Manager
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 45 mins

**Problem Statement:**
Build a bookmark management application.

**Requirements:**
```javascript
class BookmarkManager {
  constructor(container) { }
  
  addBookmark(bookmark) { }
  editBookmark(id, data) { }
  deleteBookmark(id) { }
  
  getBookmarks(options) { }
  searchBookmarks(query) { }
  filterByFolder(folder) { }
  filterByTag(tag) { }
  
  createFolder(name, parent) { }
  moveBookmark(id, folderId) { }
  
  importBookmarks(html) { }
  exportBookmarks(format) { }
  
  checkLinks() { }               // Verify URLs still work
}
```

**Features:**
- Bookmark CRUD
- Folders hierarchy
- Tags
- Search
- Import/export
- Link validation
- Favicon display

**Learning Objectives:**
- Hierarchical data
- URL handling
- Import/export formats

**Extension:** Add browser extension integration concept.

---

### Assignment I69: Memory Game
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 50 mins

**Problem Statement:**
Build a memory matching game.

**Requirements:**
```javascript
class MemoryGame {
  constructor(container, options) { }
  // options: { gridSize, theme, timeLimit }
  
  start() { }
  restart() { }
  
  flipCard(index) { }
  checkMatch() { }
  
  getScore() { }
  getMoves() { }
  getTime() { }
  
  pause() { }
  resume() { }
  
  getHighScores() { }
  saveScore(name) { }
}
```

**Features:**
- Multiple grid sizes
- Card flip animation
- Match detection
- Move counter
- Timer
- High scores
- Multiple themes

**Learning Objectives:**
- Game logic
- CSS animations
- Score tracking

**Extension:** Add multiplayer mode and custom images.

---

### Assignment I70: Drawing Canvas
**Difficulty:** ⭐⭐⭐⭐ (4/5) | **Time:** 70 mins

**Problem Statement:**
Build a basic drawing application.

**Requirements:**
```javascript
class DrawingCanvas {
  constructor(container) { }
  
  // Tools
  setTool(tool) { }           // pencil, brush, eraser, line, rectangle, circle
  setColor(color) { }
  setBrushSize(size) { }
  
  // Actions
  clear() { }
  undo() { }
  redo() { }
  fill(color) { }
  
  // File operations
  save() { }                  // Download as image
  load(image) { }
  
  // Layer management
  addLayer() { }
  removeLayer(index) { }
  selectLayer(index) { }
}
```

**Features:**
- Multiple drawing tools
- Color picker
- Brush sizes
- Undo/redo
- Clear canvas
- Save image
- Basic shapes

**Learning Objectives:**
- Canvas API
- Drawing algorithms
- Event handling for drawing

**Extension:** Add layers and image filters.

---

# 🟠 ADVANCED LEVEL

## Module 1: ES6+ Modern JavaScript

### Assignment A1: Block Scoping Deep Dive
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 30 mins

**Problem Statement:**
Explore let/const behavior in depth.

**Requirements:**
```javascript
// Demonstrate each concept:
class ScopeExplorer {
  // Temporal dead zone examples
  static temporalDeadZone() { }
  
  // Loop variable capture
  static loopClosure() { }
  
  // Block scope vs function scope
  static scopeComparison() { }
  
  // const with objects
  static constMutability() { }
  
  // Redeclaration behavior
  static redeclaration() { }
}
```

**Test Cases:**
```javascript
// Show TDZ error
console.log(x); // ReferenceError
let x = 5;

// Loop closure difference
for (var i = 0; i < 3; i++) { setTimeout(() => console.log(i), 100); } // 3, 3, 3
for (let j = 0; j < 3; j++) { setTimeout(() => console.log(j), 100); } // 0, 1, 2
```

**Learning Objectives:**
- Deep understanding of block scoping
- Temporal dead zone concept
- When to use let vs const

**Extension:** Create scope visualizer tool.

---

### Assignment A2: Advanced Destructuring
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 35 mins

**Problem Statement:**
Master complex destructuring patterns.

**Requirements:**
```javascript
// Implement these patterns:
function advancedArrayDestructuring() {
  // Nested destructuring
  // Skip elements
  // Default values
  // Rest pattern
  // Swap without temp variable
}

function advancedObjectDestructuring() {
  // Rename properties
  // Default values
  // Nested objects
  // Computed property names
  // Rest properties
}

function parameterDestructuring({ name, age = 18, ...rest }) { }

function mixedDestructuring([ first, ...rest ], { config }) { }
```

**Learning Objectives:**
- Complex destructuring patterns
- Default values with destructuring
- Parameter destructuring

**Extension:** Create a utility to auto-destructure API responses.

---

### Assignment A3: Advanced Spread/Rest
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 30 mins

**Problem Statement:**
Explore advanced spread/rest operator usage.

**Requirements:**
```javascript
class SpreadRestUtils {
  // Object merging with override order
  static mergeDeep(...objects) { }
  
  // Array operations
  static insert(arr, index, ...items) { }
  static remove(arr, ...indices) { }
  
  // Function utilities
  static partial(fn, ...presetArgs) { }
  static spread(fn) { }  // Converts array to args
  
  // Copy with modifications
  static cloneWith(obj, modifications) { }
}
```

**Test Cases:**
```javascript
SpreadRestUtils.mergeDeep(
  { a: { b: 1 } },
  { a: { c: 2 } }
) // { a: { b: 1, c: 2 } }

const add = (a, b, c) => a + b + c;
const add5 = SpreadRestUtils.partial(add, 5);
add5(3, 2) // 10
```

**Learning Objectives:**
- Deep merging with spread
- Partial application with rest
- Immutable operations

**Extension:** Implement immer-like produce function.

---

### Assignment A4: Enhanced Object Literals
**Difficulty:** ⭐⭐ (2/5) | **Time:** 25 mins

**Problem Statement:**
Use all enhanced object literal features.

**Requirements:**
```javascript
// Use all features:
const name = 'John';
const age = 30;

const person = {
  // Shorthand property
  name,
  age,
  
  // Shorthand method
  greet() { },
  
  // Computed property names
  [`prop_${Date.now()}`]: 'dynamic',
  
  // Getter/setter
  get fullName() { },
  set fullName(value) { },
  
  // Generator method
  *items() { },
  
  // Async method
  async fetchData() { }
};

// Factory function using enhanced literals
function createModel(type, properties) { }
```

**Learning Objectives:**
- All enhanced object literal features
- When to use each feature
- Cleaner object creation

**Extension:** Build a DSL using computed properties.

---

### Assignment A5: Symbols Deep Dive
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 35 mins

**Problem Statement:**
Master Symbol usage and well-known symbols.

**Requirements:**
```javascript
class SymbolUtils {
  // Create and use symbols
  static createPrivateKey(description) { }
  
  // Symbol registry
  static getShared(key) { }
  
  // Well-known symbols
  static makeIterable(obj) { }       // Symbol.iterator
  static customStringTag(obj, tag) { } // Symbol.toStringTag
  static customToPrimitive(obj) { }  // Symbol.toPrimitive
  static customSearch(obj) { }       // Symbol.search
}

// Example: Make object iterable
const range = { from: 1, to: 5 };
// After: for (const n of range) { console.log(n); } // 1, 2, 3, 4, 5
```

**Learning Objectives:**
- Create and use symbols
- Well-known symbols
- Symbol registry

**Extension:** Implement a symbol-based enum.

---

### Assignment A6: Iterators
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 35 mins

**Problem Statement:**
Create custom iterators.

**Requirements:**
```javascript
// Make these iterable:
class Range {
  constructor(start, end, step = 1) { }
  [Symbol.iterator]() { }
}

class LinkedList {
  // Make linked list iterable
}

class Tree {
  // Make tree iterable (different traversal orders)
  inorder() { }
  preorder() { }
  postorder() { }
}

// Utility iterators
function* take(iterable, n) { }
function* filter(iterable, predicate) { }
function* map(iterable, fn) { }
```

**Test Cases:**
```javascript
const range = new Range(1, 10, 2);
[...range] // [1, 3, 5, 7, 9]

const arr = [1, 2, 3, 4, 5];
[...take(filter(arr, x => x % 2), 2)] // [1, 3]
```

**Learning Objectives:**
- Implement iterator protocol
- Create lazy iterators
- Chain iterator operations

**Extension:** Implement async iterators.

---

### Assignment A7: Generators
**Difficulty:** ⭐⭐⭐⭐ (4/5) | **Time:** 45 mins

**Problem Statement:**
Master generator functions.

**Requirements:**
```javascript
// Basic generators
function* counter(start = 0) { }
function* fibonacci() { }
function* range(start, end, step) { }

// Advanced patterns
function* flatten(arr) { }           // Recursive flatten
function* walk(dir) { }              // File system walk simulation
function* partition(arr, size) { }   // Chunk generator

// Generator control
class GeneratorRunner {
  static run(generatorFn) { }        // Auto-run to completion
  static runAsync(generatorFn) { }   // Handle promises in yield
  static pool(generators, limit) { } // Concurrent execution
}
```

**Test Cases:**
```javascript
const fib = fibonacci();
fib.next().value; // 1
fib.next().value; // 1
fib.next().value; // 2
fib.next().value; // 3

[...range(0, 10, 2)] // [0, 2, 4, 6, 8]
```

**Learning Objectives:**
- Generator function syntax
- Bidirectional communication
- Generators for async control

**Extension:** Implement co-routine pattern.

---

### Assignment A8: ES6 Classes
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 35 mins

**Problem Statement:**
Master ES6 class syntax.

**Requirements:**
```javascript
class Animal {
  // Private field
  #name;
  
  // Static property
  static kingdom = 'Animalia';
  
  // Constructor
  constructor(name) { }
  
  // Instance method
  speak() { }
  
  // Getter/setter
  get name() { }
  set name(value) { }
  
  // Static method
  static create(name) { }
  
  // Private method
  #validate(name) { }
}

class Dog extends Animal {
  // Extend with super
  constructor(name, breed) { }
  
  // Override method
  speak() { }
}
```

**Learning Objectives:**
- Class syntax completely
- Private fields and methods
- Static members

**Extension:** Implement mixins with classes.

---

### Assignment A9: Class Inheritance
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 35 mins

**Problem Statement:**
Implement complex class hierarchies.

**Requirements:**
```javascript
// Implement a class hierarchy:
class Shape {
  #color;
  constructor(color) { }
  get area() { throw new Error('Implement in subclass'); }
  toString() { }
}

class Circle extends Shape {
  #radius;
}

class Rectangle extends Shape {
  #width;
  #height;
}

class Square extends Rectangle {
  // Use rectangle but enforce square
}

// Mixin pattern
const Resizable = (Base) => class extends Base {
  resize(factor) { }
};

const Movable = (Base) => class extends Base {
  move(x, y) { }
};
```

**Learning Objectives:**
- Complex inheritance
- Abstract methods pattern
- Mixins

**Extension:** Implement interfaces pattern.

---

### Assignment A10: Optional Chaining & Nullish Coalescing
**Difficulty:** ⭐⭐ (2/5) | **Time:** 25 mins

**Problem Statement:**
Master ?. and ?? operators.

**Requirements:**
```javascript
class SafeAccess {
  // Replace try/catch with ?.
  static getNestedValue(obj, path) { }
  
  // Safe method calling
  static safeCall(obj, method, ...args) { }
  
  // With arrays
  static safeArrayAccess(arr, index) { }
  
  // Nullish coalescing utilities
  static defaultTo(value, defaultValue) { }
  static defaultToMany(...values) { }  // First non-nullish
}

// Usage patterns:
const user = { profile: { name: 'John' } };
user?.profile?.name         // 'John'
user?.settings?.theme ?? 'light'  // 'light'
user?.getName?.()           // undefined (safe method call)
```

**Learning Objectives:**
- When to use ?. vs &&
- When to use ?? vs ||
- Combine operators

**Extension:** Create a utility for path-based safe access.

---

### Assignment A11: Modules System
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 40 mins

**Problem Statement:**
Master ES6 modules.

**Requirements:**
```javascript
// utils.js - Named exports
export const add = (a, b) => a + b;
export function multiply(a, b) { }
export class Calculator { }

// constants.js - Re-exports
export { PI, E } from './math.js';
export * as utils from './utils.js';

// main.js - Imports
import { add, multiply } from './utils.js';
import Calculator from './calculator.js';
import * as Utils from './utils.js';
import { default as Calc } from './calculator.js';

// Dynamic imports
async function loadModule(name) {
  const module = await import(`./modules/${name}.js`);
  return module;
}
```

**Learning Objectives:**
- Named vs default exports
- Re-exports
- Dynamic imports

**Extension:** Implement a module loader/bundler concept.

---

### Assignment A12: Sets and Maps
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 35 mins

**Problem Statement:**
Master Set and Map operations.

**Requirements:**
```javascript
class SetUtils {
  static union(setA, setB) { }
  static intersection(setA, setB) { }
  static difference(setA, setB) { }
  static symmetricDifference(setA, setB) { }
  static isSubset(setA, setB) { }
  static isSuperset(setA, setB) { }
}

class MapUtils {
  static fromObject(obj) { }
  static toObject(map) { }
  static merge(...maps) { }
  static filter(map, predicate) { }
  static mapValues(map, fn) { }
  static groupBy(items, keyFn) { }
}

// Bidirectional map
class BiMap {
  set(key, value) { }
  get(key) { }
  getValue(key) { }
  getKey(value) { }
}
```

**Learning Objectives:**
- Set operations
- Map operations
- When to use Set/Map vs Object/Array

**Extension:** Implement LRU cache with Map.

---

### Assignment A13: WeakSet and WeakMap
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 30 mins

**Problem Statement:**
Understand weak collections.

**Requirements:**
```javascript
// Private data storage
class PrivateData {
  #privateData = new WeakMap();
  
  constructor(obj) {
    this.#privateData.set(obj, {});
  }
  
  set(obj, key, value) { }
  get(obj, key) { }
}

// Object tagging
class ObjectTagger {
  #tagged = new WeakSet();
  
  tag(obj) { }
  isTagged(obj) { }
}

// Use cases demonstration:
class CacheManager {
  // Cache that allows garbage collection
}

class ProcessedRegistry {
  // Track processed objects without memory leak
}
```

**Learning Objectives:**
- WeakMap/WeakSet behavior
- Memory management benefits
- Appropriate use cases

**Extension:** Implement object metadata storage.

---

### Assignment A14: Proxy Basics
**Difficulty:** ⭐⭐⭐⭐ (4/5) | **Time:** 45 mins

**Problem Statement:**
Create useful proxies.

**Requirements:**
```javascript
// Observable object
function createObservable(target, handler) {
  // Calls handler on any change
}

// Validation proxy
function createValidated(target, schema) {
  // Validates on set
}

// Default values proxy
function withDefaults(target, defaults) {
  // Returns default if property undefined
}

// Read-only proxy
function createReadOnly(target) {
  // Throws on write attempts
}

// Logging proxy
function createLogged(target) {
  // Logs all access
}
```

**Test Cases:**
```javascript
const obj = createObservable({}, (prop, value) => {
  console.log(`${prop} changed to ${value}`);
});
obj.name = 'John'; // Logs: "name changed to John"

const user = withDefaults({}, { role: 'user', active: true });
user.role // 'user'
```

**Learning Objectives:**
- Proxy handler traps
- Create reactive objects
- Validation with proxies

**Extension:** Implement Vue-like reactivity system.

---

### Assignment A15: Reflect API
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 30 mins

**Problem Statement:**
Use Reflect API with Proxy.

**Requirements:**
```javascript
// Demonstrate Reflect methods:
class ReflectExplorer {
  // Property operations
  static getProperty(obj, key) { }
  static setProperty(obj, key, value) { }
  static deleteProperty(obj, key) { }
  static hasProperty(obj, key) { }
  
  // Object operations
  static getPrototype(obj) { }
  static setPrototype(obj, proto) { }
  static getKeys(obj) { }
  static preventExtensions(obj) { }
  static isExtensible(obj) { }
  
  // Function operations
  static apply(fn, thisArg, args) { }
  static construct(Constructor, args) { }
}

// Proper proxy forwarding
const handler = {
  get(target, prop, receiver) {
    return Reflect.get(target, prop, receiver);
  }
};
```

**Learning Objectives:**
- All Reflect methods
- When to use Reflect vs direct
- Proper proxy forwarding

**Extension:** Create a proxy wrapper utility.

---

### Assignment A16: Regex Modern Features
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 35 mins

**Problem Statement:**
Master modern regex features.

**Requirements:**
```javascript
class ModernRegex {
  // Named capture groups
  static parseDate(str) {
    const regex = /(?<year>\d{4})-(?<month>\d{2})-(?<day>\d{2})/;
    // Return { year, month, day }
  }
  
  // Lookbehind assertions
  static extractPrice(str) {
    // Match number after $
  }
  
  // Unicode property escapes
  static matchEmoji(str) { }
  
  // dotAll mode (s flag)
  static matchMultiline(str) { }
  
  // matchAll
  static findAllMatches(str, pattern) { }
}
```

**Test Cases:**
```javascript
ModernRegex.parseDate('2024-01-15')
// { year: '2024', month: '01', day: '15' }

[...ModernRegex.findAllMatches('test1 test2 test3', /test\d/g)]
// [['test1'], ['test2'], ['test3']]
```

**Learning Objectives:**
- Named capture groups
- Lookbehind assertions
- matchAll method

**Extension:** Build a regex builder with fluent API.

---

### Assignment A17: BigInt
**Difficulty:** ⭐⭐ (2/5) | **Time:** 25 mins

**Problem Statement:**
Work with BigInt.

**Requirements:**
```javascript
class BigIntUtils {
  static add(a, b) { }           // Works with number or bigint
  static multiply(a, b) { }
  static power(base, exp) { }
  static factorial(n) { }         // For large factorials
  static fibonacci(n) { }         // For large fib numbers
  
  static safeDivide(a, b) { }    // Handle precision
  static compare(a, b) { }        // Works across types
  
  static toNumber(bigint) { }    // Safe conversion
  static toBigInt(value) { }     // From various sources
}
```

**Test Cases:**
```javascript
BigIntUtils.factorial(100n)
// Returns actual value, not Infinity

BigIntUtils.fibonacci(1000n)
// Works for very large fibonacci
```

**Learning Objectives:**
- BigInt creation and operations
- Mixing with regular numbers
- When to use BigInt

**Extension:** Implement arbitrary precision decimals.

---

### Assignment A18: Array.from and Array Methods
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 30 mins

**Problem Statement:**
Master advanced array methods.

**Requirements:**
```javascript
class ArrayUtils {
  // Array.from advanced usage
  static fromIterable(iterable, mapFn) { }
  static fromLength(length, mapFn) { }
  static fromObject(obj) { }
  
  // Array methods
  static flat(arr, depth) { }
  static flatMap(arr, fn) { }
  static at(arr, index) { }
  
  // findLast and findLastIndex
  static findLast(arr, predicate) { }
  static findLastIndex(arr, predicate) { }
  
  // Array.prototype.group (proposal)
  static group(arr, fn) { }
  static groupToMap(arr, fn) { }
  
  // toSorted, toReversed, toSpliced (immutable)
  static toSorted(arr, fn) { }
  static toReversed(arr) { }
  static toSpliced(arr, start, deleteCount, ...items) { }
}
```

**Learning Objectives:**
- Array.from possibilities
- Newer array methods
- Immutable array methods

**Extension:** Implement array piping/chaining.

---

### Assignment A19: Object Methods
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 30 mins

**Problem Statement:**
Master modern Object methods.

**Requirements:**
```javascript
class ObjectUtils {
  // Object.entries/fromEntries patterns
  static transform(obj, keyFn, valueFn) { }
  static filter(obj, predicate) { }
  static map(obj, fn) { }
  
  // Object.hasOwn (replacement for hasOwnProperty)
  static hasOwn(obj, key) { }
  
  // Object.assign vs spread (deep understanding)
  static shallowMerge(...sources) { }
  static deepMerge(...sources) { }
  
  // Object.getOwnPropertyDescriptors
  static cloneWithDescriptors(obj) { }
  
  // Object.freeze/seal patterns
  static deepFreeze(obj) { }
  static deepSeal(obj) { }
}
```

**Learning Objectives:**
- Object.entries/fromEntries
- Property descriptors
- Immutability patterns

**Extension:** Implement immutable.js-like patterns.

---

### Assignment A20: String Methods
**Difficulty:** ⭐⭐ (2/5) | **Time:** 25 mins

**Problem Statement:**
Use modern string methods.

**Requirements:**
```javascript
class StringUtils {
  // New methods
  static replaceAll(str, search, replace) { }
  static at(str, index) { }
  
  // Template literal tags
  static html(strings, ...values) { }  // HTML escape
  static raw(strings, ...values) { }
  static trim(strings, ...values) { }  // Dedent multiline
  
  // String.prototype.matchAll
  static matchAll(str, regex) { }
  
  // String.prototype.normalize
  static normalizeUnicode(str) { }
  
  // padStart/padEnd patterns
  static formatNumber(num, width) { }
  static formatCurrency(amount) { }
}
```

**Learning Objectives:**
- New string methods
- Tagged template literals
- Unicode normalization

**Extension:** Create a template engine with tags.

---

### Assignment A21: Promise Extensions
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 35 mins

**Problem Statement:**
Implement Promise utilities.

**Requirements:**
```javascript
class PromiseUtils {
  // Promise.withResolvers()
  static withResolvers() { }
  
  // Timeout wrapper
  static timeout(promise, ms, message) { }
  
  // Retry with options
  static retry(fn, options) { }
  // options: { attempts, delay, backoff, retryOn }
  
  // Promise pool with concurrency
  static pool(tasks, concurrency) { }
  
  // Deferred promise
  static deferred() { }
  
  // Promise.try (proposal)
  static try(fn) { }
}
```

**Test Cases:**
```javascript
const { promise, resolve, reject } = PromiseUtils.withResolvers();

await PromiseUtils.retry(fetchUser, {
  attempts: 3,
  delay: 1000,
  backoff: 2,
  retryOn: (error) => error.status === 503
});
```

**Learning Objectives:**
- Promise utility patterns
- Retry strategies
- Concurrency control

**Extension:** Implement cancellable promises.

---

### Assignment A22: Async Iteration
**Difficulty:** ⭐⭐⭐⭐ (4/5) | **Time:** 40 mins

**Problem Statement:**
Master async iterators and generators.

**Requirements:**
```javascript
// Async generator
async function* paginate(fetchFn, options) {
  // Yield pages until no more
}

// Async iterator
class AsyncQueue {
  async *[Symbol.asyncIterator]() { }
  enqueue(item) { }
  close() { }
}

// Utilities
class AsyncIterUtils {
  static async *map(asyncIterable, fn) { }
  static async *filter(asyncIterable, predicate) { }
  static async *take(asyncIterable, n) { }
  static async collect(asyncIterable) { }
  static async reduce(asyncIterable, fn, initial) { }
}
```

**Test Cases:**
```javascript
for await (const page of paginate(fetchUsers, { pageSize: 10 })) {
  processPage(page);
}

const queue = new AsyncQueue();
setTimeout(() => queue.enqueue(1), 100);
setTimeout(() => queue.enqueue(2), 200);
setTimeout(() => queue.close(), 300);

for await (const item of queue) {
  console.log(item); // 1, 2
}
```

**Learning Objectives:**
- Async generators
- for-await-of
- Stream-like processing

**Extension:** Implement ReadableStream wrapper.

---

## Module 2: Object-Oriented Programming

### Assignment A23: Prototypes Deep Dive
**Difficulty:** ⭐⭐⭐⭐ (4/5) | **Time:** 45 mins

**Problem Statement:**
Understand prototypes completely.

**Requirements:**
```javascript
class PrototypeExplorer {
  // Demonstrate prototype chain
  static getPrototypeChain(obj) { }
  
  // Create inheritance without class
  static createInheritance(parent, child) { }
  
  // Prototype methods
  static addMethod(Constructor, name, fn) { }
  
  // Property shadowing
  static demonstrateShadowing() { }
  
  // Performance implications
  static compareInstanceVsPrototype() { }
}

// Manual prototype setup
function Animal(name) { this.name = name; }
Animal.prototype.speak = function() { };

function Dog(name, breed) { 
  Animal.call(this, name);
  this.breed = breed;
}
// Set up inheritance manually
```

**Learning Objectives:**
- Prototype chain completely
- Manual inheritance setup
- Prototype vs instance properties

**Extension:** Visualize prototype chains.

---

### Assignment A24: Constructor Functions
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 30 mins

**Problem Statement:**
Master constructor function patterns.

**Requirements:**
```javascript
// Constructor function patterns
function User(name, email) {
  // Handle called without new
  if (!(this instanceof User)) {
    return new User(name, email);
  }
  
  // Private via closure
  let _password;
  
  // Public properties
  this.name = name;
  this.email = email;
  
  // Privileged method
  this.setPassword = function(pwd) { _password = pwd; };
  this.checkPassword = function(pwd) { return pwd === _password; };
}

// Static methods
User.create = function(data) { };
User.validate = function(user) { };

// Prototype methods
User.prototype.greet = function() { };
```

**Learning Objectives:**
- Constructor function patterns
- new.target usage
- Prototype vs instance methods

**Extension:** Create a class decorator system.

---

### Assignment A25: Object.create Patterns
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 30 mins

**Problem Statement:**
Use Object.create effectively.

**Requirements:**
```javascript
// Prototypal inheritance
const animal = {
  speak() { console.log(`${this.name} makes a sound`); }
};

const dog = Object.create(animal, {
  name: { value: 'Dog', writable: true },
  breed: { value: 'Unknown', writable: true, enumerable: true }
});

// Null prototype objects
const nullProto = Object.create(null);

// Mixin pattern with Object.create
function mixin(target, ...sources) { }

// Factory with Object.create
function createPerson(name, age) {
  const proto = {
    greet() { },
    toString() { }
  };
  return Object.create(proto, { /* ... */ });
}
```

**Learning Objectives:**
- Object.create vs class
- Property descriptors
- Null prototype objects

**Extension:** Implement trait system.

---

### Assignment A26: Property Descriptors
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 35 mins

**Problem Statement:**
Control property behavior.

**Requirements:**
```javascript
class PropertyController {
  // Define computed property
  static defineComputed(obj, key, getter, setter) { }
  
  // Make property non-writable
  static makeReadOnly(obj, key) { }
  
  // Make property non-enumerable
  static hide(obj, key) { }
  
  // Make property non-configurable
  static lock(obj, key) { }
  
  // Clone with descriptors
  static cloneExact(obj) { }
  
  // Property validators
  static defineValidated(obj, key, validator) { }
}

// Example: Age that must be positive
PropertyController.defineValidated(user, 'age', (value) => {
  if (typeof value !== 'number' || value < 0) {
    throw new TypeError('Age must be positive number');
  }
  return value;
});
```

**Learning Objectives:**
- Property descriptor flags
- defineProperty/defineProperties
- getOwnPropertyDescriptor

**Extension:** Implement observable properties.

---

### Assignment A27: Getters and Setters
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 30 mins

**Problem Statement:**
Use getters/setters effectively.

**Requirements:**
```javascript
class User {
  #firstName;
  #lastName;
  #email;
  
  // Computed property
  get fullName() { }
  set fullName(value) { }
  
  // Validated setter
  get email() { }
  set email(value) { }
  
  // Lazy initialization
  get profile() { }
  
  // Cached computed
  get statistics() { }
  invalidateCache() { }
}

// Utility: Define lazy getter
function defineLazy(obj, key, initializer) { }

// Utility: Define memoized getter
function defineMemoized(obj, key, calculator) { }
```

**Learning Objectives:**
- Computed properties
- Validation in setters
- Lazy initialization pattern

**Extension:** Implement reactive getters.

---

### Assignment A28: Static Methods and Properties
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 25 mins

**Problem Statement:**
Use static members effectively.

**Requirements:**
```javascript
class DatabaseConnection {
  // Static instance (Singleton)
  static #instance;
  static getInstance() { }
  
  // Static configuration
  static config = {};
  static configure(options) { }
  
  // Factory methods
  static create(options) { }
  static createFromEnv() { }
  
  // Static utilities
  static isValidUrl(url) { }
  static parseUrl(url) { }
  
  // Static initialization block
  static {
    // Complex initialization
  }
}

// Inheritance of static methods
class PostgresConnection extends DatabaseConnection {
  static createFromEnv() { }  // Override
}
```

**Learning Objectives:**
- Static methods/properties
- Factory pattern with static
- Static initialization blocks

**Extension:** Implement static registry pattern.

---

### Assignment A29: Private Fields Deep Dive
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 30 mins

**Problem Statement:**
Master private class features.

**Requirements:**
```javascript
class BankAccount {
  // Private fields
  #balance = 0;
  #transactions = [];
  
  // Private static
  static #instances = new Map();
  
  // Private methods
  #validate(amount) { }
  #log(action) { }
  
  // Private accessors
  get #formattedBalance() { }
  
  // Public API using private internals
  deposit(amount) { }
  withdraw(amount) { }
  getBalance() { }
  
  // Static factory using private
  static get(id) {
    return BankAccount.#instances.get(id);
  }
}

// Check for private field existence
function hasBankAccount(obj) {
  return #balance in obj;  // Private brand check
}
```

**Learning Objectives:**
- Private fields completely
- Private methods
- Private brand checks

**Extension:** Compare with WeakMap approach.

---

### Assignment A30: The 'this' Keyword
**Difficulty:** ⭐⭐⭐⭐ (4/5) | **Time:** 40 mins

**Problem Statement:**
Master 'this' in all contexts.

**Requirements:**
```javascript
class ThisExplorer {
  // Default binding
  static defaultBinding() { }
  
  // Implicit binding
  static implicitBinding() { }
  
  // Explicit binding (call, apply, bind)
  static explicitBinding() { }
  
  // new binding
  static newBinding() { }
  
  // Arrow function lexical this
  static arrowFunctions() { }
  
  // Event handler this
  static eventHandlers() { }
  
  // Common pitfalls and fixes
  static pitfalls() { }
}

// Practical scenarios
class Counter {
  count = 0;
  
  // Problem: loses this
  increment() { this.count++; }
  
  // Solution 1: Arrow in class field
  incrementArrow = () => { this.count++; };
  
  // Solution 2: Bind in constructor
  constructor() {
    this.increment = this.increment.bind(this);
  }
}
```

**Learning Objectives:**
- All this binding rules
- Arrow function behavior
- Fix this issues

**Extension:** Create this binding visualizer.

---

### Assignment A31: call, apply, bind
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 30 mins

**Problem Statement:**
Master function context methods.

**Requirements:**
```javascript
class ContextUtils {
  // Implement from scratch
  static myCall(fn, context, ...args) { }
  static myApply(fn, context, args) { }
  static myBind(fn, context, ...boundArgs) { }
  
  // Practical uses
  static borrowMethod(obj, otherObj, method) { }
  static partialApply(fn, ...partialArgs) { }
  
  // Method borrowing patterns
  static arrayLikeToArray(arrayLike) { }
  static maxOfArray(arr) { }
}

// Usage patterns
const obj = {
  multiplier: 2,
  multiply(a, b) { return (a + b) * this.multiplier; }
};

const boundMultiply = ContextUtils.myBind(obj.multiply, obj, 5);
boundMultiply(3); // 16
```

**Learning Objectives:**
- Implement call/apply/bind
- Method borrowing
- Partial application

**Extension:** Implement soft binding.

---

### Assignment A32: Closures Advanced
**Difficulty:** ⭐⭐⭐⭐ (4/5) | **Time:** 45 mins

**Problem Statement:**
Master closure patterns.

**Requirements:**
```javascript
// Module pattern
const Module = (function() {
  // Private state
  let count = 0;
  
  return {
    increment() { count++; },
    getCount() { return count; }
  };
})();

// Function factory
function createMultiplier(factor) {
  return function(n) { return n * factor; };
}

// Once/memoize pattern
function once(fn) { }
function memoize(fn) { }

// Closure with WeakMap for private data
const privateData = new WeakMap();
class SecureObject {
  constructor() {
    privateData.set(this, {});
  }
}

// Closure pitfalls
function closurePitfall() {
  const functions = [];
  for (var i = 0; i < 3; i++) {
    functions.push(function() { return i; });
  }
  // All return 3!
}
```

**Learning Objectives:**
- Closure memory model
- Module pattern
- Common pitfalls

**Extension:** Analyze closure memory usage.

---

### Assignment A33: Pure Functions
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 30 mins

**Problem Statement:**
Implement pure function patterns.

**Requirements:**
```javascript
// Check if function is pure
function isPure(fn) {
  // Static analysis concept
}

// Convert impure to pure
const sum = (() => {
  let total = 0;
  return (n) => { total += n; return total; };
})();

// Pure version
function pureSum(numbers) { }

// Pure transformations
const PureUtils = {
  // Array operations (non-mutating)
  push(arr, item) { },
  pop(arr) { },
  update(arr, index, item) { },
  remove(arr, index) { },
  
  // Object operations (non-mutating)
  set(obj, key, value) { },
  unset(obj, key) { },
  update(obj, key, fn) { }
};
```

**Learning Objectives:**
- Pure function characteristics
- Convert impure to pure
- Immutable operations

**Extension:** Implement structural sharing.

---

### Assignment A34: Higher-Order Functions Advanced
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 35 mins

**Problem Statement:**
Advanced HOF patterns.

**Requirements:**
```javascript
class HOFUtils {
  // Compose functions
  static compose(...fns) { }
  static pipe(...fns) { }
  
  // Currying utilities
  static curry(fn) { }
  static uncurry(fn) { }
  
  // Partial application
  static partial(fn, ...args) { }
  static partialRight(fn, ...args) { }
  
  // Function modification
  static flip(fn) { }  // Flip first two args
  static negate(predicate) { }
  static complement(predicate) { }
  
  // Async HOFs
  static asyncCompose(...fns) { }
  static asyncPipe(...fns) { }
}
```

**Test Cases:**
```javascript
const fn = HOFUtils.compose(
  x => x * 2,
  x => x + 1,
  x => x ** 2
);
fn(3); // ((3 ** 2) + 1) * 2 = 20

const curriedAdd = HOFUtils.curry((a, b, c) => a + b + c);
curriedAdd(1)(2)(3); // 6
```

**Learning Objectives:**
- Function composition
- Currying implementation
- Combinator patterns

**Extension:** Implement point-free utilities.

---

### Assignment A35: Memoization Deep Dive
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 35 mins

**Problem Statement:**
Implement advanced memoization.

**Requirements:**
```javascript
class Memoization {
  // Basic memoization
  static memoize(fn) { }
  
  // With custom key
  static memoizeWith(keyFn, fn) { }
  
  // With TTL (expiring cache)
  static memoizeTTL(fn, ttl) { }
  
  // With max size (LRU)
  static memoizeLRU(fn, maxSize) { }
  
  // Async memoization
  static memoizeAsync(fn) { }
  
  // Weak memoization (object keys)
  static memoizeWeak(fn) { }
  
  // Cache control
  static createMemoized(fn, options) {
    return {
      fn: /* memoized function */,
      clear: () => { },
      size: () => { }
    };
  }
}
```

**Test Cases:**
```javascript
const fibonacci = Memoization.memoize((n) => {
  if (n <= 1) return n;
  return fibonacci(n - 1) + fibonacci(n - 2);
});

fibonacci(50); // Fast now
```

**Learning Objectives:**
- Memoization strategies
- Cache invalidation
- Memory management

**Extension:** Implement distributed memoization concept.

---

## Module 3: Browser APIs and Advanced Projects

### Assignment A36: Error Handling Advanced
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 35 mins

**Problem Statement:**
Implement comprehensive error handling.

**Requirements:**
```javascript
// Custom error hierarchy
class AppError extends Error { }
class ValidationError extends AppError { }
class NetworkError extends AppError { }
class AuthError extends AppError { }

// Error utilities
class ErrorHandler {
  static wrap(fn) { }               // Return [error, result]
  static wrapAsync(fn) { }
  static retry(fn, options) { }
  static fallback(fn, fallbackFn) { }
  static timeout(fn, ms) { }
  
  // Global handling
  static registerGlobalHandler() { }
  static logError(error, context) { }
  static reportError(error) { }
}
```

**Learning Objectives:**
- Error class hierarchies
- Error wrapping patterns
- Global error handling

**Extension:** Add error tracking service integration.

---

### Assignment A37: Web Workers
**Difficulty:** ⭐⭐⭐⭐ (4/5) | **Time:** 50 mins

**Problem Statement:**
Use Web Workers for heavy computation.

**Requirements:**
```javascript
class WorkerPool {
  constructor(workerScript, size) { }
  
  async execute(task) { }
  async executeAll(tasks) { }
  
  terminate() { }
  resize(newSize) { }
}

// Inline worker creation
class InlineWorker {
  static create(fn) { }
  static async run(fn, args) { }
}

// Offload heavy tasks
const heavyTasks = {
  async sortLargeArray(arr) { },
  async processImage(imageData) { },
  async calculatePrimes(limit) { }
};
```

**Learning Objectives:**
- Create and manage workers
- Transfer data to workers
- Worker pools

**Extension:** Add SharedArrayBuffer usage.

---

### Assignment A38: Intersection Observer
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 35 mins

**Problem Statement:**
Master IntersectionObserver for visibility tracking.

**Requirements:**
```javascript
class VisibilityTracker {
  constructor(options) { }
  
  observe(element, callback) { }
  unobserve(element) { }
  disconnect() { }
  
  // Helpers
  static onVisible(element, callback) { }
  static onHidden(element, callback) { }
  static lazyLoad(elements, loadFn) { }
  static infiniteScroll(sentinel, loadMore) { }
  static trackReadTime(elements) { }
}
```

**Learning Objectives:**
- Configure IntersectionObserver
- Handle visibility changes
- Practical applications

**Extension:** Create scroll-based animations.

---

### Assignment A39: Mutation Observer
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 30 mins

**Problem Statement:**
Track DOM mutations with MutationObserver.

**Requirements:**
```javascript
class DOMWatcher {
  constructor(target, options) { }
  
  onAdd(callback) { }      // Child added
  onRemove(callback) { }   // Child removed
  onChange(callback) { }   // Attribute change
  onText(callback) { }     // Text change
  
  disconnect() { }
  
  // Utilities
  static watchAttribute(element, attr, callback) { }
  static watchChildren(element, callback) { }
  static waitForElement(selector) { }  // Promise-based
}
```

**Learning Objectives:**
- Configure MutationObserver
- Handle different mutation types
- Wait for dynamic content

**Extension:** Build DOM diffing utility.

---

### Assignment A40: Performance API
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 35 mins

**Problem Statement:**
Use Performance API for measurements.

**Requirements:**
```javascript
class PerformanceUtils {
  // Timing functions
  static measure(name, fn) { }
  static measureAsync(name, fn) { }
  static mark(name) { }
  static measureBetween(start, end) { }
  
  // Performance entries
  static getResourceTimings() { }
  static getNavigationTiming() { }
  static getLongTasks() { }
  
  // Frame timing
  static measureFPS(duration) { }
  
  // Reporting
  static generateReport() { }
}
```

**Learning Objectives:**
- Performance marks and measures
- Navigation timing
- Resource timing

**Extension:** Create performance dashboard.

---

### Assignment A41: Canvas API
**Difficulty:** ⭐⭐⭐⭐ (4/5) | **Time:** 55 mins

**Problem Statement:**
Create graphics with Canvas API.

**Requirements:**
```javascript
class CanvasUtils {
  constructor(canvas) { }
  
  // Drawing
  drawLine(x1, y1, x2, y2, style) { }
  drawRect(x, y, w, h, style) { }
  drawCircle(cx, cy, r, style) { }
  drawPath(points, style) { }
  drawText(text, x, y, style) { }
  
  // Image manipulation
  drawImage(img, x, y, w, h) { }
  getImageData(x, y, w, h) { }
  putImageData(data, x, y) { }
  
  // Transformations
  rotate(angle) { }
  scale(x, y) { }
  translate(x, y) { }
  
  // Effects
  applyFilter(filter) { }
  toDataURL(type) { }
}
```

**Learning Objectives:**
- Canvas drawing methods
- Image manipulation
- Transforms and state

**Extension:** Create image filters.

---

### Assignment A42: Geolocation API
**Difficulty:** ⭐⭐ (2/5) | **Time:** 25 mins

**Problem Statement:**
Work with Geolocation API.

**Requirements:**
```javascript
class GeoLocation {
  static async getCurrentPosition(options) {
    // Return { lat, lng, accuracy, ... }
  }
  
  static watchPosition(callback, options) {
    // Return unsubscribe function
  }
  
  static async getAddress(lat, lng) { }  // Reverse geocoding
  static async getCoordinates(address) { }  // Forward geocoding
  
  static calculateDistance(pos1, pos2) { }  // Haversine
  static isNearby(pos1, pos2, radius) { }
}
```

**Learning Objectives:**
- Get user location
- Watch position changes
- Distance calculations

**Extension:** Build location tracker.

---

### Assignment A43: History API
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 35 mins

**Problem Statement:**
Build SPA routing with History API.

**Requirements:**
```javascript
class Router {
  constructor(routes) { }
  // routes: { '/': Component, '/about': Component, ... }
  
  navigate(path) { }
  back() { }
  forward() { }
  replace(path) { }
  
  onRouteChange(callback) { }
  
  getCurrentRoute() { }
  getParams() { }
  getQuery() { }
  
  // Middleware
  beforeEach(guard) { }
  afterEach(hook) { }
}
```

**Learning Objectives:**
- pushState/replaceState
- Handle popstate
- Build client-side routing

**Extension:** Add route guards and lazy loading.

---

### Assignment A44: File API
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 35 mins

**Problem Statement:**
Work with files in the browser.

**Requirements:**
```javascript
class FileUtils {
  static async readAsText(file) { }
  static async readAsDataURL(file) { }
  static async readAsArrayBuffer(file) { }
  static async readAsJSON(file) { }
  
  static download(data, filename, type) { }
  static createBlob(data, type) { }
  static createObjectURL(blob) { }
  static revokeObjectURL(url) { }
  
  // Validation
  static isImage(file) { }
  static isValidSize(file, maxBytes) { }
  static isValidType(file, allowedTypes) { }
}
```

**Learning Objectives:**
- FileReader usage
- Blob and Object URLs
- File validation

**Extension:** Add progress tracking for large files.

---

### Assignment A45: Notifications API
**Difficulty:** ⭐⭐ (2/5) | **Time:** 25 mins

**Problem Statement:**
Implement browser notifications.

**Requirements:**
```javascript
class Notifications {
  static async requestPermission() { }
  static hasPermission() { }
  
  static show(title, options) { }
  // options: { body, icon, tag, data, onClick, onClose }
  
  static close(notification) { }
  static closeAll() { }
  
  // Scheduled notifications
  static schedule(title, options, delay) { }
  static cancelScheduled(id) { }
}
```

**Learning Objectives:**
- Request notification permission
- Create notifications
- Handle notification events

**Extension:** Add push notification setup.

---

### Assignment A46: Implementing Debounce/Throttle
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 35 mins

**Problem Statement:**
Implement debounce and throttle from scratch.

**Requirements:**
```javascript
function debounce(fn, wait, options = {}) {
  // options: { leading, trailing, maxWait }
  // Return debounced function with cancel() and flush()
}

function throttle(fn, wait, options = {}) {
  // options: { leading, trailing }
  // Return throttled function with cancel()
}

// Additional utilities
function rafThrottle(fn) { }  // Use requestAnimationFrame
function debouncePromise(fn, wait) { }  // Return promise
function leadingEdge(fn, wait) { }  // Execute immediately
```

**Learning Objectives:**
- Implement debounce correctly
- Implement throttle correctly
- Handle edge cases

**Extension:** Add visualizer for timing.

---

### Assignment A47: Implementing Deep Clone
**Difficulty:** ⭐⭐⭐⭐ (4/5) | **Time:** 45 mins

**Problem Statement:**
Implement deep cloning for complex objects.

**Requirements:**
```javascript
function deepClone(value, options = {}) {
  // Handle all primitives
  // Handle Arrays
  // Handle Objects
  // Handle Date, RegExp, Map, Set
  // Handle Circular references
  // Handle Symbols
  // Handle functions (optionally)
}

// Specialized cloners
function cloneWithTransform(obj, transform) { }
function cloneOmitting(obj, keys) { }
function cloneWith(obj, overrides) { }
```

**Test Cases:**
```javascript
const original = {
  date: new Date(),
  regex: /test/gi,
  map: new Map([[1, 'a']]),
  nested: { deep: { value: 1 } }
};
original.circular = original;

const cloned = deepClone(original);
// Should be deep equal but not same reference
```

**Learning Objectives:**
- Handle all JavaScript types
- Circular reference detection
- Performance considerations

**Extension:** Compare with structuredClone.

---

### Assignment A48: Implementing Event Emitter
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 35 mins

**Problem Statement:**
Build a complete EventEmitter.

**Requirements:**
```javascript
class EventEmitter {
  on(event, listener) { }
  off(event, listener) { }
  once(event, listener) { }
  emit(event, ...args) { }
  
  // Advanced features
  prependListener(event, listener) { }
  removeAllListeners(event) { }
  listenerCount(event) { }
  eventNames() { }
  getListeners(event) { }
  
  // Wildcards
  onAny(listener) { }     // Listen to all events
  offAny(listener) { }
}
```

**Test Cases:**
```javascript
const emitter = new EventEmitter();
emitter.on('data', (d) => console.log(d));
emitter.once('connect', () => console.log('connected'));
emitter.emit('data', { value: 1 });
```

**Learning Objectives:**
- Pub/sub implementation
- Memory management
- Event handling patterns

**Extension:** Add typed events with TypeScript-like checking.

---

### Assignment A49: Implementing Promise
**Difficulty:** ⭐⭐⭐⭐⭐ (5/5) | **Time:** 60 mins

**Problem Statement:**
Implement Promise from scratch.

**Requirements:**
```javascript
class MyPromise {
  constructor(executor) { }
  
  then(onFulfilled, onRejected) { }
  catch(onRejected) { }
  finally(onFinally) { }
  
  static resolve(value) { }
  static reject(reason) { }
  static all(promises) { }
  static race(promises) { }
  static allSettled(promises) { }
  static any(promises) { }
}
```

**Must Pass:**
- Promises/A+ test suite concepts
- Chaining
- Error handling
- Microtask scheduling

**Learning Objectives:**
- Promise internals
- Microtask queue
- State machine

**Extension:** Implement async/await transpilation concept.

---

### Assignment A50: Implementing Observable
**Difficulty:** ⭐⭐⭐⭐ (4/5) | **Time:** 50 mins

**Problem Statement:**
Build RxJS-like Observable.

**Requirements:**
```javascript
class Observable {
  constructor(subscribe) { }
  
  subscribe(observer) { }
  // observer: { next, error, complete }
  
  // Operators
  pipe(...operators) { }
  
  // Creation
  static of(...values) { }
  static from(iterable) { }
  static fromEvent(element, event) { }
  static interval(ms) { }
}

// Operators
const map = (fn) => (source) => { };
const filter = (predicate) => (source) => { };
const take = (count) => (source) => { };
const debounceTime = (ms) => (source) => { };
```

**Learning Objectives:**
- Observable pattern
- Operators concept
- Stream processing

**Extension:** Add more operators.

---

## Module 4: Advanced Projects

### Assignment A51: Kanban Board
**Difficulty:** ⭐⭐⭐⭐ (4/5) | **Time:** 90 mins

**Problem Statement:**
Build a Kanban board with drag and drop.

**Requirements:**
- Multiple columns (Todo, In Progress, Done)
- Drag cards between columns
- Add/edit/delete cards
- Column customization
- Persist to localStorage
- Keyboard accessibility

**Learning Objectives:**
- Drag and drop API
- Complex state management
- Data persistence

**Extension:** Add swimlanes and WIP limits.

---

### Assignment A52: Real-time Chat Interface
**Difficulty:** ⭐⭐⭐⭐ (4/5) | **Time:** 90 mins

**Problem Statement:**
Build a chat application interface.

**Requirements:**
- Message list with timestamps
- Message input with send
- Typing indicators
- Read receipts
- Message reactions
- File attachments (UI only)
- Simulated real-time updates

**Learning Objectives:**
- Real-time patterns
- Message queuing
- UI state management

**Extension:** Add WebSocket integration.

---

### Assignment A53: Spreadsheet Application
**Difficulty:** ⭐⭐⭐⭐⭐ (5/5) | **Time:** 120 mins

**Problem Statement:**
Build a basic spreadsheet.

**Requirements:**
- Cell grid with editing
- Formula support (basic: SUM, AVG)
- Cell references (A1, B2)
- Dependency tracking
- Keyboard navigation
- Copy/paste support

**Learning Objectives:**
- Formula parsing
- Dependency graph
- Complex UI interactions

**Extension:** Add more functions and formatting.

---

### Assignment A54: JSON Editor/Viewer
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 60 mins

**Problem Statement:**
Build a JSON editor with tree view.

**Requirements:**
- Tree view for objects/arrays
- Expand/collapse nodes
- Inline editing
- Add/remove properties
- Validation
- Format/minify
- Copy path

**Learning Objectives:**
- Recursive rendering
- Tree manipulation
- JSON validation

**Extension:** Add diff view.

---

### Assignment A55: Calculator with Expression Parsing
**Difficulty:** ⭐⭐⭐⭐ (4/5) | **Time:** 75 mins

**Problem Statement:**
Build a calculator that parses expressions.

**Requirements:**
- Parse expressions like "2 + 3 * 4"
- Operator precedence
- Parentheses support
- Variables
- Functions (sin, cos, sqrt)
- History

**Learning Objectives:**
- Expression parsing
- Operator precedence
- Interpreter pattern

**Extension:** Add graphing capability.

---

### Assignment A56: State Management Library
**Difficulty:** ⭐⭐⭐⭐⭐ (5/5) | **Time:** 90 mins

**Problem Statement:**
Build a Redux-like state manager.

**Requirements:**
```javascript
const store = createStore(
  reducer,
  initialState,
  enhancers
);

store.getState();
store.dispatch(action);
store.subscribe(listener);

// Middleware support
applyMiddleware(logger, thunk)
```

**Learning Objectives:**
- State management patterns
- Middleware concept
- Time-travel debugging

**Extension:** Add computed values.

---

### Assignment A57: Markdown Parser
**Difficulty:** ⭐⭐⭐⭐ (4/5) | **Time:** 75 mins

**Problem Statement:**
Build a markdown to HTML parser.

**Requirements:**
- Headings, paragraphs
- Bold, italic, code
- Links, images
- Lists (ordered, unordered)
- Code blocks
- Blockquotes

**Learning Objectives:**
- Text parsing
- Regular expressions
- AST concept

**Extension:** Add syntax highlighting.

---

### Assignment A58: Virtual DOM Implementation
**Difficulty:** ⭐⭐⭐⭐⭐ (5/5) | **Time:** 120 mins

**Problem Statement:**
Implement basic virtual DOM.

**Requirements:**
```javascript
// Create virtual nodes
const vdom = h('div', { class: 'container' }, [
  h('h1', {}, ['Title']),
  h('p', {}, ['Content'])
]);

// Render to real DOM
render(vdom, container);

// Diff and patch
const newVdom = h('div', { class: 'container' }, [...]);
patch(oldVdom, newVdom, container);
```

**Learning Objectives:**
- Virtual DOM concept
- Diffing algorithm
- Efficient DOM updates

**Extension:** Add keyed children and components.

---

### Assignment A59: Form Validation Library
**Difficulty:** ⭐⭐⭐⭐ (4/5) | **Time:** 75 mins

**Problem Statement:**
Build a validation library.

**Requirements:**
```javascript
const schema = {
  email: [required(), email()],
  password: [required(), minLength(8), pattern(/[A-Z]/)],
  age: [required(), min(18), max(100)],
  website: [optional(), url()],
  confirmPassword: [equalTo('password')]
};

const result = validate(data, schema);
// { valid: false, errors: { ... } }
```

**Learning Objectives:**
- Schema-based validation
- Composable validators
- Async validation

**Extension:** Add form binding.

---

### Assignment A60: Component Framework
**Difficulty:** ⭐⭐⭐⭐⭐ (5/5) | **Time:** 120 mins

**Problem Statement:**
Build a mini component framework.

**Requirements:**
```javascript
class Component {
  constructor(props) { }
  
  // Lifecycle
  onMount() { }
  onUpdate() { }
  onDestroy() { }
  
  // State
  setState(updates) { }
  
  // Required
  render() { }
}

// Usage
class Counter extends Component {
  state = { count: 0 };
  
  render() {
    return `<button>${this.state.count}</button>`;
  }
}
```

**Learning Objectives:**
- Component lifecycle
- State management
- Rendering optimization

**Extension:** Add hooks-like API.

---

### Assignment A61: Data Visualization Library
**Difficulty:** ⭐⭐⭐⭐ (4/5) | **Time:** 90 mins

**Problem Statement:**
Build a charting library.

**Requirements:**
```javascript
const chart = new Chart(container, {
  type: 'bar', // bar, line, pie
  data: { ... },
  options: { ... }
});

chart.update(newData);
chart.resize();
chart.destroy();
```

**Chart Types:**
- Bar chart
- Line chart
- Pie chart
- Each with labels, legends, tooltips

**Learning Objectives:**
- SVG or Canvas drawing
- Data-driven visualization
- Responsive charts

**Extension:** Add animations.

---

### Assignment A62: Tic-Tac-Toe with AI
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 60 mins

**Problem Statement:**
Build Tic-Tac-Toe with minimax AI.

**Requirements:**
- 3x3 grid display
- Player vs AI
- Unbeatable AI (minimax)
- Win/draw detection
- Score tracking
- Difficulty levels

**Learning Objectives:**
- Game logic
- Minimax algorithm
- AI decision making

**Extension:** Add 4x4 version.

---

### Assignment A63: Snake Game
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 60 mins

**Problem Statement:**
Build the classic Snake game.

**Requirements:**
- Snake movement with controls
- Food spawning
- Collision detection
- Score tracking
- Speed increase
- High scores

**Learning Objectives:**
- Game loop
- Collision detection
- Canvas animation

**Extension:** Add power-ups and obstacles.

---

### Assignment A64: URL Shortener (UI)
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 45 mins

**Problem Statement:**
Build URL shortener frontend.

**Requirements:**
- Input for long URL
- Generate short code
- Display shortened URL
- Copy to clipboard
- History of shortened URLs
- QR code generation (optional)

**Learning Objectives:**
- Form handling
- Unique ID generation
- Clipboard API

**Extension:** Add analytics display.

---

### Assignment A65: Code Editor (Basic)
**Difficulty:** ⭐⭐⭐⭐ (4/5) | **Time:** 75 mins

**Problem Statement:**
Build a basic code editor.

**Requirements:**
- Textarea with line numbers
- Tab handling
- Auto-indent
- Bracket matching
- Find/replace
- Keyboard shortcuts

**Learning Objectives:**
- Text manipulation
- Keyboard handling
- Editor UX

**Extension:** Add syntax highlighting.

---

### Assignment A66: TypeAhead Search
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 50 mins

**Problem Statement:**
Build an advanced typeahead.

**Requirements:**
- Debounced input
- Async data fetching
- Highlight matching text
- Keyboard navigation
- Recent searches
- Categories/grouping
- Cache results

**Learning Objectives:**
- Search optimization
- Result presentation
- Performance

**Extension:** Add fuzzy matching.

---

### Assignment A67: Image Filter App
**Difficulty:** ⭐⭐⭐⭐ (4/5) | **Time:** 60 mins

**Problem Statement:**
Build image filter application.

**Requirements:**
- Upload image
- Apply filters (grayscale, blur, etc.)
- Adjust brightness/contrast
- Compare before/after
- Download result

**Learning Objectives:**
- Canvas image manipulation
- Pixel operations
- Filter algorithms

**Extension:** Add custom filter creation.

---

### Assignment A68: Password Manager (UI)
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 55 mins

**Problem Statement:**
Build password manager UI.

**Requirements:**
- Add/edit/delete entries
- Categories
- Password generator
- Search and filter
- Show/hide passwords
- Copy to clipboard
- Export/import

**Learning Objectives:**
- Secure data handling
- Local encryption concept
- UX for sensitive data

**Extension:** Add master password.

---

### Assignment A69: File Explorer
**Difficulty:** ⭐⭐⭐⭐ (4/5) | **Time:** 70 mins

**Problem Statement:**
Build a file explorer UI.

**Requirements:**
- Tree view sidebar
- Grid/list view
- Breadcrumb navigation
- Create/rename/delete
- Drag and drop
- Context menu
- Search

**Learning Objectives:**
- Tree data structures
- File system metaphor
- Complex interactions

**Extension:** Add file previews.

---

### Assignment A70: Pomodoro Timer App
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 50 mins

**Problem Statement:**
Build Pomodoro productivity timer.

**Requirements:**
- Work/break timers
- Customizable durations
- Audio notifications
- Session tracking
- Statistics
- Keyboard shortcuts
- Background operation

**Learning Objectives:**
- Timer management
- Background processing
- Productivity features

**Extension:** Add task integration.

---

# 🔴 EXPERT LEVEL

## Module 1: Design Patterns

### Assignment E1: Singleton Pattern
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 30 mins

**Problem Statement:**
Implement Singleton pattern variations.

**Requirements:**
```javascript
// Lazy Singleton
class Database {
  static #instance;
  static getInstance() { }
}

// Module Singleton (ES modules)
let instance;
export function getConnection() { }

// Singleton with options
class Logger {
  static #instance;
  static getInstance(options) { }
  static resetInstance() { }  // For testing
}
```

**Learning Objectives:**
- Singleton implementation
- Lazy initialization
- Thread safety concepts

**Extension:** Compare with service locator pattern.

---

### Assignment E2: Factory Pattern
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 35 mins

**Problem Statement:**
Implement Factory and Abstract Factory patterns.

**Requirements:**
```javascript
// Simple Factory
class VehicleFactory {
  static create(type, options) { }
}

// Factory Method
class Dialog {
  createButton() { throw new Error('Override'); }
  render() { }
}

class WindowsDialog extends Dialog { }
class MacDialog extends Dialog { }

// Abstract Factory
class GUIFactory {
  createButton() { }
  createCheckbox() { }
}

class WindowsFactory extends GUIFactory { }
class MacFactory extends GUIFactory { }
```

**Learning Objectives:**
- Factory method pattern
- Abstract factory pattern
- Object creation patterns

**Extension:** Add type registration system.

---

### Assignment E3: Builder Pattern
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 35 mins

**Problem Statement:**
Implement Builder pattern.

**Requirements:**
```javascript
class QueryBuilder {
  select(...fields) { return this; }
  from(table) { return this; }
  where(condition) { return this; }
  orderBy(field, direction) { return this; }
  limit(n) { return this; }
  build() { }
}

// Usage:
const query = new QueryBuilder()
  .select('id', 'name')
  .from('users')
  .where('active = true')
  .orderBy('name', 'asc')
  .limit(10)
  .build();

// Director
class RequestBuilder { }
class ResponseBuilder { }
```

**Learning Objectives:**
- Fluent interface
- Step-by-step construction
- Immutable builders

**Extension:** Add validation in build.

---

### Assignment E4: Prototype Pattern
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 30 mins

**Problem Statement:**
Implement Prototype pattern.

**Requirements:**
```javascript
// Clone interface
class Shape {
  clone() { }
}

class Circle extends Shape {
  constructor(radius, color) { }
  clone() { }
}

// Prototype registry
class ShapeRegistry {
  #prototypes = new Map();
  
  register(name, prototype) { }
  get(name) { }
  create(name, modifications) { }
}
```

**Learning Objectives:**
- Prototype pattern concept
- Deep vs shallow clone
- Prototype registry

**Extension:** Add clone customization.

---

### Assignment E5: Observer Pattern
**Difficulty:** ⭐⭐⭐⭐ (4/5) | **Time:** 45 mins

**Problem Statement:**
Implement comprehensive Observer pattern.

**Requirements:**
```javascript
class Subject {
  #observers = new Set();
  
  subscribe(observer) { }
  unsubscribe(observer) { }
  notify(data) { }
}

// With filter
class FilterableSubject extends Subject {
  subscribeWhen(predicate, observer) { }
}

// With async
class AsyncSubject extends Subject {
  async notifyAsync(data) { }
}

// Observable property
class Observable {
  static observe(obj) { }
  static unobserve(obj) { }
}
```

**Learning Objectives:**
- Observer pattern
- Subscription management
- Memory leak prevention

**Extension:** Add RxJS-like operators.

---

### Assignment E6: Pub/Sub Pattern
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 35 mins

**Problem Statement:**
Implement Pub/Sub (Event Bus).

**Requirements:**
```javascript
class EventBus {
  static subscribe(event, callback) { }
  static publish(event, data) { }
  static unsubscribe(event, callback) { }
  
  // Async publish
  static async publishAsync(event, data) { }
  
  // Wildcard subscriptions
  static subscribePattern(pattern, callback) { }
  
  // Once
  static once(event, callback) { }
  
  // Debug
  static listSubscriptions() { }
}
```

**Learning Objectives:**
- Decoupled communication
- Global event handling
- Pattern matching

**Extension:** Add event replay and persistence.

---

### Assignment E7: Strategy Pattern
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 35 mins

**Problem Statement:**
Implement Strategy pattern.

**Requirements:**
```javascript
// Payment strategies
class PaymentProcessor {
  #strategy;
  
  setStrategy(strategy) { }
  process(amount) { }
}

const creditCard = {
  process(amount) { }
};

const paypal = {
  process(amount) { }
};

// Validation strategies
class Validator {
  static strategies = { };
  
  addStrategy(name, fn) { }
  validate(data, strategyNames) { }
}
```

**Learning Objectives:**
- Interchangeable algorithms
- Open/closed principle
- Runtime flexibility

**Extension:** Add strategy selection based on data.

---

### Assignment E8: Command Pattern
**Difficulty:** ⭐⭐⭐⭐ (4/5) | **Time:** 45 mins

**Problem Statement:**
Implement Command pattern with undo.

**Requirements:**
```javascript
// Command interface
class Command {
  execute() { }
  undo() { }
}

// Concrete commands
class AddTextCommand extends Command { }
class DeleteTextCommand extends Command { }
class FormatTextCommand extends Command { }

// Command invoker with history
class CommandManager {
  #history = [];
  #undone = [];
  
  execute(command) { }
  undo() { }
  redo() { }
  canUndo() { }
  canRedo() { }
}

// Macro command
class MacroCommand extends Command { }
```

**Learning Objectives:**
- Command encapsulation
- Undo/redo implementation
- Command queueing

**Extension:** Add command serialization.

---

### Assignment E9: Decorator Pattern
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 35 mins

**Problem Statement:**
Implement Decorator pattern.

**Requirements:**
```javascript
// Base
class Coffee {
  getCost() { }
  getDescription() { }
}

// Decorators
class MilkDecorator extends Coffee {
  #coffee;
  constructor(coffee) { }
}

class SugarDecorator extends Coffee { }
class WhipDecorator extends Coffee { }

// Usage:
const coffee = new WhipDecorator(
  new MilkDecorator(
    new SimpleCoffee()
  )
);

// Function decorator
function withLogging(fn) { }
function withMemoization(fn) { }
function withRetry(fn, attempts) { }
```

**Learning Objectives:**
- Decorator composition
- Function decorators
- Single responsibility

**Extension:** Add decorator registry.

---

### Assignment E10: Adapter Pattern
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 30 mins

**Problem Statement:**
Implement Adapter pattern.

**Requirements:**
```javascript
// Target interface
class MediaPlayer {
  play(filename) { }
}

// Adaptees (incompatible)
class VLCPlayer {
  playVLC(filename) { }
}

class MP4Player {
  playMP4(filename) { }
}

// Adapters
class VLCAdapter extends MediaPlayer {
  #player;
  constructor() { this.#player = new VLCPlayer(); }
  play(filename) { this.#player.playVLC(filename); }
}

// API adapter
class LegacyAPIAdapter {
  static adapt(oldResponse) { }
}
```

**Learning Objectives:**
- Interface adaptation
- Legacy integration
- Third-party wrapping

**Extension:** Add two-way adapter.

---

### Assignment E11: Facade Pattern
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 30 mins

**Problem Statement:**
Implement Facade pattern.

**Requirements:**
```javascript
// Complex subsystems
class VideoFile { }
class Codec { }
class CompressionCodec { }
class AudioMixer { }
class BitrateReader { }

// Facade
class VideoConverter {
  convert(filename, format) {
    // Orchestrates all subsystems
  }
}

// API Facade
class APIfacade {
  static async fetchUserWithDetails(userId) {
    // Combines multiple API calls
  }
}
```

**Learning Objectives:**
- Simplify complex systems
- Reduce coupling
- Clean API design

**Extension:** Add facade layering.

---

### Assignment E12: Proxy Pattern
**Difficulty:** ⭐⭐⭐⭐ (4/5) | **Time:** 40 mins

**Problem Statement:**
Implement various Proxy patterns.

**Requirements:**
```javascript
// Virtual Proxy (lazy loading)
class LazyImage {
  #realImage;
  constructor(filename) { }
  get image() { }  // Loads on first access
}

// Protection Proxy
class SecureDocument {
  #document;
  #accessLevel;
  
  view() { }
  edit() { }  // Only if accessLevel permits
}

// Caching Proxy
class CachedAPI {
  #cache = new Map();
  #api;
  
  fetch(url) { }  // Return cached if available
}

// Logging Proxy
function createLoggingProxy(target) { }
```

**Learning Objectives:**
- Virtual proxy
- Protection proxy
- Caching proxy

**Extension:** Add remote proxy concept.

---

### Assignment E13: Module Pattern
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 30 mins

**Problem Statement:**
Implement Module pattern variations.

**Requirements:**
```javascript
// IIFE Module
const Calculator = (function() {
  // Private
  let result = 0;
  
  // Public API
  return {
    add(n) { },
    getResult() { }
  };
})();

// Revealing Module
const Utils = (function() {
  function privateHelper() { }
  function publicMethod() { }
  
  return { publicMethod };
})();

// ES6 Module pattern
export const createModule = (options) => {
  const state = { };
  return { /* public API */ };
};
```

**Learning Objectives:**
- Encapsulation
- Information hiding
- Clean interfaces

**Extension:** Add module dependency injection.

---

### Assignment E14: State Pattern
**Difficulty:** ⭐⭐⭐⭐ (4/5) | **Time:** 45 mins

**Problem Statement:**
Implement State pattern.

**Requirements:**
```javascript
// State interface
class State {
  handle(context) { }
}

// Concrete states
class DraftState extends State { }
class PendingState extends State { }
class PublishedState extends State { }

// Context
class Document {
  #state;
  
  setState(state) { }
  publish() { }
  review() { }
  reject() { }
}

// Alternative: State Machine
class StateMachine {
  #states;
  #current;
  #transitions;
  
  transition(action) { }
  canTransition(action) { }
}
```

**Learning Objectives:**
- State management
- Finite state machines
- State transitions

**Extension:** Add state history.

---

### Assignment E15: Mediator Pattern
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 35 mins

**Problem Statement:**
Implement Mediator pattern.

**Requirements:**
```javascript
// Mediator
class ChatRoom {
  #users = new Map();
  
  register(user) { }
  send(message, from, to) { }
  broadcast(message, from) { }
}

// Colleague
class User {
  #mediator;
  #name;
  
  send(message, to) { }
  receive(message, from) { }
}

// UI Mediator
class FormMediator {
  // Coordinates form fields
}
```

**Learning Objectives:**
- Centralized communication
- Reduce coupling
- Component coordination

**Extension:** Add message filtering.

---

### Assignment E16: Chain of Responsibility
**Difficulty:** ⭐⭐⭐⭐ (4/5) | **Time:** 40 mins

**Problem Statement:**
Implement Chain of Responsibility.

**Requirements:**
```javascript
// Handler
class Handler {
  #next;
  
  setNext(handler) { this.#next = handler; return handler; }
  handle(request) { }
}

// Concrete handlers
class AuthHandler extends Handler { }
class ValidationHandler extends Handler { }
class LoggingHandler extends Handler { }
class ProcessHandler extends Handler { }

// Usage:
const pipeline = new AuthHandler();
pipeline
  .setNext(new ValidationHandler())
  .setNext(new LoggingHandler())
  .setNext(new ProcessHandler());

pipeline.handle(request);
```

**Learning Objectives:**
- Request pipeline
- Middleware pattern
- Loose coupling

**Extension:** Add async chain support.

---

### Assignment E17: Iterator Pattern
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 35 mins

**Problem Statement:**
Implement custom iterators.

**Requirements:**
```javascript
class Tree {
  // Different iteration strategies
  inOrderIterator() { }
  preOrderIterator() { }
  postOrderIterator() { }
  levelOrderIterator() { }
}

class PaginatedCollection {
  // Iterate through pages
  async *[Symbol.asyncIterator]() { }
}

// Iterator utilities
function* concat(...iterables) { }
function* interleave(...iterables) { }
function* cycle(iterable) { }
function* enumerate(iterable) { }
```

**Learning Objectives:**
- Iterator protocol
- Custom iteration strategies
- Lazy evaluation

**Extension:** Add bidirectional iterator.

---

### Assignment E18: Visitor Pattern
**Difficulty:** ⭐⭐⭐⭐ (4/5) | **Time:** 45 mins

**Problem Statement:**
Implement Visitor pattern.

**Requirements:**
```javascript
// Element
class Shape {
  accept(visitor) { }
}

class Circle extends Shape {
  accept(visitor) { visitor.visitCircle(this); }
}

class Rectangle extends Shape {
  accept(visitor) { visitor.visitRectangle(this); }
}

// Visitors
class AreaCalculator {
  visitCircle(circle) { }
  visitRectangle(rect) { }
}

class Renderer {
  visitCircle(circle) { }
  visitRectangle(rect) { }
}

// AST Visitor
class ASTVisitor { }
```

**Learning Objectives:**
- Double dispatch
- Open/closed principle
- AST processing

**Extension:** Add visitor composition.

---

### Assignment E19: Flyweight Pattern
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 35 mins

**Problem Statement:**
Implement Flyweight pattern for memory optimization.

**Requirements:**
```javascript
// Flyweight
class CharacterStyle {
  #font;
  #color;
  #size;
  
  static #cache = new Map();
  
  static get(font, color, size) {
    const key = `${font}-${color}-${size}`;
    if (!this.#cache.has(key)) {
      this.#cache.set(key, new CharacterStyle(font, color, size));
    }
    return this.#cache.get(key);
  }
}

// Context
class Character {
  #char;
  #style;  // Shared flyweight
  #position;  // Unique
}

// Factory
class ParticleFactory { }
```

**Learning Objectives:**
- Memory optimization
- Intrinsic vs extrinsic state
- Object pooling

**Extension:** Add flyweight statistics.

---

### Assignment E20: Composite Pattern
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 35 mins

**Problem Statement:**
Implement Composite pattern.

**Requirements:**
```javascript
// Component
class FileSystemItem {
  getName() { }
  getSize() { }
}

// Leaf
class File extends FileSystemItem {
  #name;
  #size;
}

// Composite
class Directory extends FileSystemItem {
  #children = [];
  
  add(item) { }
  remove(item) { }
  getSize() { }  // Sum of all children
  getChildren() { }
}

// UI Component Tree
class UIComponent {
  render() { }
  addChild(component) { }
}
```

**Learning Objectives:**
- Tree structures
- Uniform treatment
- Recursive composition

**Extension:** Add traversal methods.

---

## Module 2: Performance and Security

### Assignment E21: Time Complexity Optimization
**Difficulty:** ⭐⭐⭐⭐ (4/5) | **Time:** 45 mins

**Problem Statement:**
Optimize code for better time complexity.

**Requirements:**
```javascript
// O(n²) → O(n) optimizations
function findDuplicatesOptimized(arr) { }  // Use Set

// O(n) → O(log n) optimizations
function binarySearchOptimized(arr, target) { }

// O(n) → O(1) optimizations
function fibonacciOptimized(n) { }  // Memoization/Matrix

// Optimize these:
function findPairsWithSum(arr, sum) { }
function longestSubstringWithoutRepeat(str) { }
function mergeIntervals(intervals) { }
```

**Learning Objectives:**
- Big O analysis
- Algorithm optimization
- Data structure selection

**Extension:** Add benchmark comparison.

---

### Assignment E22: Space Complexity Optimization
**Difficulty:** ⭐⭐⭐⭐ (4/5) | **Time:** 40 mins

**Problem Statement:**
Optimize memory usage.

**Requirements:**
```javascript
// In-place algorithms
function reverseInPlace(arr) { }
function deduplicateInPlace(arr) { }

// Streaming/chunked processing
function processLargeFile(file, chunkSize) { }
function* streamProcess(data) { }

// Memory-efficient structures
class CircularBuffer { }
class SparseMatrix { }
class BitSet { }
```

**Learning Objectives:**
- In-place algorithms
- Streaming processing
- Memory-efficient structures

**Extension:** Add memory profiling.

---

### Assignment E23: DOM Performance
**Difficulty:** ⭐⭐⭐⭐ (4/5) | **Time:** 45 mins

**Problem Statement:**
Optimize DOM operations.

**Requirements:**
```javascript
class DOMOptimizer {
  // Batch reads and writes
  static batchUpdate(operations) { }
  
  // Virtual scrolling
  static createVirtualList(container, items, rowHeight) { }
  
  // Efficient rendering
  static useDocumentFragment(elements) { }
  
  // Avoid layout thrashing
  static measureThenMutate(measureFn, mutateFn) { }
  
  // Event delegation for performance
  static setupDelegation(container, handler) { }
}
```

**Learning Objectives:**
- Avoid layout thrashing
- Virtual scrolling
- Batch DOM operations

**Extension:** Add performance metrics.

---

### Assignment E24: Request Optimization
**Difficulty:** ⭐⭐⭐⭐ (4/5) | **Time:** 45 mins

**Problem Statement:**
Optimize network requests.

**Requirements:**
```javascript
class RequestOptimizer {
  // Request deduplication
  static dedupe(fetchFn) { }
  
  // Request batching
  static batch(requests, delay) { }
  
  // Request caching
  static cache(fetchFn, ttl) { }
  
  // Request priority queue
  static createPriorityQueue() { }
  
  // Prefetching
  static prefetch(urls) { }
  
  // Progressive loading
  static loadProgressive(chunks) { }
}
```

**Learning Objectives:**
- Request deduplication
- Batching and caching
- Prefetching strategies

**Extension:** Add offline support.

---

### Assignment E25: Lazy Loading Patterns
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 35 mins

**Problem Statement:**
Implement lazy loading strategies.

**Requirements:**
```javascript
// Lazy module loading
const loadModule = async (name) => {
  return await import(`./modules/${name}.js`);
};

// Lazy component
class LazyComponent {
  static load(importFn) { }
}

// Lazy property
function lazyProperty(obj, key, initializer) { }

// Route-based lazy loading
class LazyRouter {
  route(path, componentLoader) { }
}

// Image lazy loading
class LazyImageLoader {
  observe(images) { }
}
```

**Learning Objectives:**
- Code splitting
- Dynamic imports
- Resource prioritization

**Extension:** Add preload hints.

---

### Assignment E26: Memory Management
**Difficulty:** ⭐⭐⭐⭐ (4/5) | **Time:** 45 mins

**Problem Statement:**
Avoid memory leaks.

**Requirements:**
```javascript
// Common memory leak patterns and fixes
class LeakPatterns {
  // Fix: Global event listeners
  static boundHandlers = new WeakMap();
  
  // Fix: Forgotten timers
  static trackedTimers = new Set();
  
  // Fix: Closures holding references
  static cleanClosure() { }
  
  // Fix: Detached DOM nodes
  static cleanupDOM() { }
  
  // Fix: Console in production
  static safeLog() { }
}

// Cleanup utility
class CleanupManager {
  add(cleanup) { }
  cleanup() { }
}
```

**Learning Objectives:**
- Memory leak patterns
- WeakMap/WeakSet usage
- Cleanup patterns

**Extension:** Add memory monitoring.

---

### Assignment E27: XSS Prevention
**Difficulty:** ⭐⭐⭐⭐ (4/5) | **Time:** 45 mins

**Problem Statement:**
Prevent XSS vulnerabilities.

**Requirements:**
```javascript
class XSSPrevention {
  // HTML encoding
  static encodeHTML(str) { }
  
  // Attribute encoding
  static encodeAttribute(str) { }
  
  // JavaScript encoding
  static encodeJS(str) { }
  
  // URL encoding
  static encodeURL(str) { }
  
  // Sanitize HTML
  static sanitize(html, allowedTags) { }
  
  // CSP header builder
  static buildCSP(policy) { }
  
  // Safe innerHTML alternative
  static safeInnerHTML(element, html) { }
}
```

**Learning Objectives:**
- XSS attack vectors
- Encoding strategies
- Content Security Policy

**Extension:** Add DOM purify implementation.

---

### Assignment E28: CSRF Protection
**Difficulty:** ⭐⭐⭐⭐ (4/5) | **Time:** 40 mins

**Problem Statement:**
Implement CSRF protection.

**Requirements:**
```javascript
class CSRFProtection {
  // Token generation
  static generateToken() { }
  
  // Token storage
  static setToken(token) { }
  static getToken() { }
  
  // Token validation (concept)
  static validateToken(token) { }
  
  // Fetch wrapper with CSRF
  static fetch(url, options) { }
  
  // Form protection
  static protectForm(form) { }
}
```

**Learning Objectives:**
- CSRF attack vectors
- Token-based protection
- SameSite cookies

**Extension:** Add double submit cookie pattern.

---

### Assignment E29: Input Validation
**Difficulty:** ⭐⭐⭐⭐ (4/5) | **Time:** 40 mins

**Problem Statement:**
Implement secure input validation.

**Requirements:**
```javascript
class InputValidator {
  // Sanitization
  static sanitizeString(str) { }
  static sanitizeNumber(str) { }
  static sanitizeEmail(str) { }
  static sanitizeURL(str) { }
  
  // Validation
  static isValidEmail(email) { }
  static isValidPhone(phone) { }
  static isValidPassword(password, policy) { }
  static isValidURL(url) { }
  
  // SQL injection prevention (concept)
  static escapeSQLParams(params) { }
  
  // Path traversal prevention
  static sanitizePath(path) { }
}
```

**Learning Objectives:**
- Input sanitization
- Validation patterns
- Injection prevention

**Extension:** Add custom validation rules.

---

### Assignment E30: Secure Storage
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 35 mins

**Problem Statement:**
Implement secure client-side storage.

**Requirements:**
```javascript
class SecureStorage {
  // Encrypted storage (concept with Web Crypto)
  static async encrypt(data, key) { }
  static async decrypt(data, key) { }
  
  // Secure cookie handling
  static setCookie(name, value, options) { }
  // options: httpOnly, secure, sameSite
  
  // Sensitive data handling
  static storeSecure(key, value) { }
  static retrieveSecure(key) { }
  static clearSecure() { }
  
  // Token storage best practices
  static storeToken(token) { }
  static clearToken() { }
}
```

**Learning Objectives:**
- Web Crypto API
- Secure cookie options
- Token storage patterns

**Extension:** Add key derivation.

---

### Assignment E31: Debounce/Throttle Implementation
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 30 mins

**Problem Statement:**
Production-ready debounce/throttle.

**Requirements:**
```javascript
function debounce(fn, wait, options = {}) {
  // Leading edge option
  // Trailing edge option
  // Max wait option
  // Cancel method
  // Flush method
  // Pending check
}

function throttle(fn, wait, options = {}) {
  // Leading edge option
  // Trailing edge option  
  // Cancel method
  // RAF variant
}
```

**Learning Objectives:**
- Complete implementation
- Edge case handling
- Production quality

**Extension:** Add async support.

---

### Assignment E32: LRU Cache Implementation
**Difficulty:** ⭐⭐⭐⭐ (4/5) | **Time:** 45 mins

**Problem Statement:**
Implement LRU cache with all features.

**Requirements:**
```javascript
class LRUCache {
  constructor(capacity) { }
  
  get(key) { }
  put(key, value) { }
  delete(key) { }
  has(key) { }
  
  clear() { }
  size() { }
  keys() { }
  values() { }
  
  // TTL support
  setWithTTL(key, value, ttl) { }
  
  // Statistics
  getStats() { }
}
```

**Learning Objectives:**
- LRU algorithm
- Efficient implementation (Map + doubly linked list)
- Cache statistics

**Extension:** Add LFU variant.

---

### Assignment E33: Object Pool Implementation
**Difficulty:** ⭐⭐⭐⭐ (4/5) | **Time:** 40 mins

**Problem Statement:**
Implement object pool for performance.

**Requirements:**
```javascript
class ObjectPool {
  constructor(factory, reset, initialSize) { }
  
  acquire() { }      // Get object from pool
  release(obj) { }   // Return to pool
  
  getSize() { }      // Current pool size
  getAvailable() { } // Available objects
  getInUse() { }     // Objects in use
  
  drain() { }        // Clear pool
  prefill(count) { } // Prefill pool
}

// Example usage:
const particlePool = new ObjectPool(
  () => new Particle(),
  (p) => p.reset(),
  100
);
```

**Learning Objectives:**
- Object pooling
- Resource reuse
- GC optimization

**Extension:** Add pool auto-scaling.

---

### Assignment E34: Service Worker Basics
**Difficulty:** ⭐⭐⭐⭐ (4/5) | **Time:** 50 mins

**Problem Statement:**
Implement basic Service Worker.

**Requirements:**
```javascript
// service-worker.js
const CACHE_NAME = 'v1';

self.addEventListener('install', (event) => {
  // Cache static assets
});

self.addEventListener('fetch', (event) => {
  // Cache-first strategy
  // Network-first strategy
  // Stale-while-revalidate
});

self.addEventListener('activate', (event) => {
  // Clean up old caches
});

// Registration helper
class ServiceWorkerManager {
  static async register() { }
  static async unregister() { }
  static async update() { }
}
```

**Learning Objectives:**
- Service Worker lifecycle
- Caching strategies
- Offline support

**Extension:** Add push notifications.

---

### Assignment E35: Web Vitals Monitoring
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 35 mins

**Problem Statement:**
Monitor Core Web Vitals.

**Requirements:**
```javascript
class WebVitals {
  static measureLCP(callback) { }   // Largest Contentful Paint
  static measureFID(callback) { }   // First Input Delay
  static measureCLS(callback) { }   // Cumulative Layout Shift
  
  static measureTTFB(callback) { }  // Time to First Byte
  static measureFCP(callback) { }   // First Contentful Paint
  
  // All vitals
  static measureAll(callback) { }
  
  // Reporting
  static report(metrics) { }
  
  // Thresholds
  static evaluate(metrics) { }
}
```

**Learning Objectives:**
- Core Web Vitals
- Performance monitoring
- User experience metrics

**Extension:** Add trend tracking.

---

### Assignment E36: Code Splitting
**Difficulty:** ⭐⭐⭐⭐ (4/5) | **Time:** 45 mins

**Problem Statement:**
Implement code splitting patterns.

**Requirements:**
```javascript
// Route-based splitting
const routes = {
  '/': () => import('./pages/Home.js'),
  '/about': () => import('./pages/About.js'),
  '/dashboard': () => import('./pages/Dashboard.js')
};

// Component lazy loading
function lazyLoad(importFn) {
  return async function() {
    const component = await importFn();
    return component.default;
  };
}

// Preloading
function preload(importFn) { }

// Bundle analyzer concept
function analyzeBundle(modules) { }
```

**Learning Objectives:**
- Dynamic imports
- Route-based splitting
- Component chunking

**Extension:** Add loading states.

---

### Assignment E37: Tree Shaking
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 35 mins

**Problem Statement:**
Write tree-shakeable code.

**Requirements:**
```javascript
// Good: Named exports
export const add = (a, b) => a + b;
export const subtract = (a, b) => a - b;

// Bad: Default export with everything
export default { add, subtract };

// Good: Side-effect free
export function pure(x) { return x * 2; }

// Tree-shakeable library structure
// index.js - re-exports only
export { add } from './math/add.js';
export { subtract } from './math/subtract.js';

// Package.json sideEffects: false concept
```

**Learning Objectives:**
- ES module benefits
- Side-effect free code
- Library structure

**Extension:** Add bundle analysis.

---

### Assignment E38: Authentication Flow
**Difficulty:** ⭐⭐⭐⭐ (4/5) | **Time:** 50 mins

**Problem Statement:**
Implement auth flow with JWT.

**Requirements:**
```javascript
class AuthService {
  // Token management
  static getAccessToken() { }
  static setAccessToken(token) { }
  static getRefreshToken() { }
  static setRefreshToken(token) { }
  
  // Auth flow
  static async login(credentials) { }
  static async logout() { }
  static async refreshToken() { }
  
  // Token validation
  static isTokenExpired(token) { }
  static decodeToken(token) { }
  
  // Axios/fetch interceptor
  static setupInterceptor(client) { }
}
```

**Learning Objectives:**
- JWT structure
- Token refresh
- Secure storage

**Extension:** Add OAuth flow.

---

### Assignment E39: Rate Limiter
**Difficulty:** ⭐⭐⭐⭐ (4/5) | **Time:** 40 mins

**Problem Statement:**
Implement client-side rate limiting.

**Requirements:**
```javascript
class RateLimiter {
  // Token bucket
  static createTokenBucket(rate, capacity) { }
  
  // Sliding window
  static createSlidingWindow(limit, windowMs) { }
  
  // Fixed window
  static createFixedWindow(limit, windowMs) { }
  
  // Usage
  static async throttledFetch(url, limiter) { }
  
  // Decorator
  static withRateLimit(fn, limiter) { }
}
```

**Learning Objectives:**
- Rate limiting algorithms
- Token bucket
- Sliding window

**Extension:** Add distributed rate limiting concept.

---

### Assignment E40: Error Boundary Pattern
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 35 mins

**Problem Statement:**
Implement error boundary pattern.

**Requirements:**
```javascript
class ErrorBoundary {
  #onError;
  #fallback;
  
  constructor(options) { }
  
  wrap(fn) { }
  wrapAsync(fn) { }
  
  static create(options) { }
}

// Global error handling
class GlobalErrorHandler {
  static setup() { }
  
  static handleError(error) { }
  static handleRejection(reason) { }
  
  static addHandler(handler) { }
  static removeHandler(handler) { }
}

// Usage:
const boundary = ErrorBoundary.create({
  onError: (error) => logError(error),
  fallback: () => showErrorUI()
});
```

**Learning Objectives:**
- Error containment
- Graceful degradation
- Recovery strategies

**Extension:** Add error retry.

---

## Module 3: Architecture and Testing

### Assignment E41: Dependency Injection
**Difficulty:** ⭐⭐⭐⭐ (4/5) | **Time:** 45 mins

**Problem Statement:**
Implement DI container.

**Requirements:**
```javascript
class Container {
  #services = new Map();
  
  register(name, factory, options) { }
  // options: { singleton, lazy, scope }
  
  resolve(name) { }
  
  createScope() { }
  
  // Decorators concept
  registerDecorator(name, decorator) { }
}

// Usage:
const container = new Container();
container.register('logger', () => new Logger());
container.register('userService', (c) => new UserService(c.resolve('logger')));

const userService = container.resolve('userService');
```

**Learning Objectives:**
- Dependency injection
- Inversion of control
- Service lifetime

**Extension:** Add auto-wiring.

---

### Assignment E42: Event Sourcing
**Difficulty:** ⭐⭐⭐⭐⭐ (5/5) | **Time:** 60 mins

**Problem Statement:**
Implement event sourcing pattern.

**Requirements:**
```javascript
class EventStore {
  #events = [];
  
  append(event) { }
  getEvents(aggregateId) { }
  getEventsByType(type) { }
  getEventsAfter(timestamp) { }
}

class Aggregate {
  #version = 0;
  #changes = [];
  
  apply(event) { }
  loadFromHistory(events) { }
  getUncommittedChanges() { }
}

// Example: Account aggregate
class Account extends Aggregate {
  #balance = 0;
  
  deposit(amount) { }
  withdraw(amount) { }
  
  // Event handlers
  onMoneyDeposited(event) { }
  onMoneyWithdrawn(event) { }
}
```

**Learning Objectives:**
- Event sourcing concept
- Aggregate pattern
- Event replay

**Extension:** Add snapshots.

---

### Assignment E43: CQRS Pattern
**Difficulty:** ⭐⭐⭐⭐⭐ (5/5) | **Time:** 55 mins

**Problem Statement:**
Implement CQRS pattern.

**Requirements:**
```javascript
// Command side
class CommandBus {
  register(commandType, handler) { }
  dispatch(command) { }
}

class CreateUserCommand { }
class CreateUserHandler {
  handle(command) { }
}

// Query side
class QueryBus {
  register(queryType, handler) { }
  dispatch(query) { }
}

class GetUserQuery { }
class GetUserHandler {
  handle(query) { }
}

// Separate read/write models
class WriteModel { }
class ReadModel { }
```

**Learning Objectives:**
- CQRS pattern
- Command/query separation
- Read optimization

**Extension:** Add eventual consistency.

---

### Assignment E44: Plugin Architecture
**Difficulty:** ⭐⭐⭐⭐ (4/5) | **Time:** 50 mins

**Problem Statement:**
Build extensible plugin system.

**Requirements:**
```javascript
class PluginManager {
  #plugins = new Map();
  #hooks = new Map();
  
  register(plugin) { }
  unregister(pluginName) { }
  
  // Lifecycle
  async initializeAll() { }
  async destroyAll() { }
  
  // Hooks
  registerHook(hookName) { }
  addHookHandler(hookName, handler) { }
  executeHook(hookName, ...args) { }
}

// Plugin interface
const myPlugin = {
  name: 'myPlugin',
  version: '1.0.0',
  init(app) { },
  destroy() { },
  hooks: {
    'beforeRender': (data) => { }
  }
};
```

**Learning Objectives:**
- Plugin architecture
- Hook system
- Extensibility

**Extension:** Add plugin dependencies.

---

### Assignment E45: Middleware Architecture
**Difficulty:** ⭐⭐⭐⭐ (4/5) | **Time:** 45 mins

**Problem Statement:**
Implement middleware system.

**Requirements:**
```javascript
class MiddlewareManager {
  #middlewares = [];
  
  use(middleware) { }
  
  async execute(context) { }
}

// Middleware signature
const loggingMiddleware = async (ctx, next) => {
  console.log('Before');
  await next();
  console.log('After');
};

// Conditional middleware
const conditionalMiddleware = (condition) => {
  return async (ctx, next) => {
    if (condition(ctx)) {
      // apply middleware
    }
    await next();
  };
};

// Error handling middleware
const errorMiddleware = async (ctx, next) => {
  try {
    await next();
  } catch (error) {
    ctx.error = error;
  }
};
```

**Learning Objectives:**
- Middleware pattern
- Async composition
- Context passing

**Extension:** Add middleware groups.

---

### Assignment E46: Repository Pattern
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 40 mins

**Problem Statement:**
Implement Repository pattern.

**Requirements:**
```javascript
// Generic repository
class Repository {
  async findById(id) { }
  async findAll(criteria) { }
  async save(entity) { }
  async delete(id) { }
  async exists(id) { }
}

// Concrete repository
class UserRepository extends Repository {
  async findByEmail(email) { }
  async findByRole(role) { }
}

// Unit of Work
class UnitOfWork {
  #repositories = new Map();
  #changes = [];
  
  getRepository(type) { }
  registerNew(entity) { }
  registerDirty(entity) { }
  registerDeleted(entity) { }
  async commit() { }
  rollback() { }
}
```

**Learning Objectives:**
- Repository pattern
- Unit of Work
- Data access abstraction

**Extension:** Add query builder integration.

---

### Assignment E47: Specification Pattern
**Difficulty:** ⭐⭐⭐⭐ (4/5) | **Time:** 40 mins

**Problem Statement:**
Implement Specification pattern.

**Requirements:**
```javascript
class Specification {
  isSatisfiedBy(candidate) { }
  
  and(other) { }
  or(other) { }
  not() { }
}

// Concrete specifications
class PriceRangeSpec extends Specification {
  constructor(min, max) { }
  isSatisfiedBy(product) { }
}

class InStockSpec extends Specification {
  isSatisfiedBy(product) { }
}

class CategorySpec extends Specification {
  constructor(category) { }
  isSatisfiedBy(product) { }
}

// Usage:
const spec = new PriceRangeSpec(10, 100)
  .and(new InStockSpec())
  .and(new CategorySpec('electronics'));

products.filter(p => spec.isSatisfiedBy(p));
```

**Learning Objectives:**
- Specification pattern
- Business rules encapsulation
- Composable criteria

**Extension:** Add SQL generation.

---

### Assignment E48: Unit Testing Patterns
**Difficulty:** ⭐⭐⭐⭐ (4/5) | **Time:** 50 mins

**Problem Statement:**
Implement testing utilities.

**Requirements:**
```javascript
// Test runner concept
class TestRunner {
  describe(description, fn) { }
  it(description, testFn) { }
  beforeEach(fn) { }
  afterEach(fn) { }
  
  async run() { }
  getResults() { }
}

// Assertions
class Assert {
  static equal(actual, expected) { }
  static deepEqual(actual, expected) { }
  static throws(fn, errorType) { }
  static async rejects(promise, errorType) { }
}

// Mocking
class Mock {
  static fn(implementation) { }
  static spy(object, method) { }
  static stub(object, method, returnValue) { }
}

// Test doubles
class TestDouble {
  static createDummy() { }
  static createFake(implementation) { }
  static createStub(methods) { }
  static createMock(expectations) { }
}
```

**Learning Objectives:**
- Test structure
- Assertions
- Mocking/stubbing

**Extension:** Add code coverage concept.

---

### Assignment E49: Integration Testing
**Difficulty:** ⭐⭐⭐⭐ (4/5) | **Time:** 45 mins

**Problem Statement:**
Implement integration test utilities.

**Requirements:**
```javascript
// API testing
class APITestClient {
  constructor(baseUrl) { }
  
  async get(path, options) { }
  async post(path, body, options) { }
  
  // Assertions
  assertStatus(response, status) { }
  assertBody(response, expected) { }
  assertHeader(response, name, value) { }
}

// DOM testing
class DOMTestUtils {
  static render(html) { }
  static query(selector) { }
  static click(element) { }
  static type(element, text) { }
  static waitFor(condition) { }
}

// Test fixtures
class FixtureManager {
  static load(name) { }
  static save(name, data) { }
  static cleanup() { }
}
```

**Learning Objectives:**
- Integration testing
- API testing
- DOM testing

**Extension:** Add snapshot testing.

---

### Assignment E50: Functional Programming
**Difficulty:** ⭐⭐⭐⭐ (4/5) | **Time:** 50 mins

**Problem Statement:**
Implement FP utilities.

**Requirements:**
```javascript
const FP = {
  // Composition
  compose: (...fns) => { },
  pipe: (...fns) => { },
  
  // Currying
  curry: (fn) => { },
  partial: (fn, ...args) => { },
  
  // Functors
  map: (fn) => (functor) => { },
  filter: (fn) => (functor) => { },
  reduce: (fn, initial) => (functor) => { },
  
  // Monads (simplified)
  Maybe: class Maybe { },
  Either: class Either { },
  
  // Utilities
  identity: (x) => x,
  constant: (x) => () => x,
  tap: (fn) => (x) => { fn(x); return x; }
};
```

**Learning Objectives:**
- FP fundamentals
- Function composition
- Maybe/Either monads

**Extension:** Add Task monad.

---

## Module 4: Expert Capstone Projects

### Assignment E51: Build a Framework
**Difficulty:** ⭐⭐⭐⭐⭐ (5/5) | **Time:** 180 mins

**Problem Statement:**
Build a mini front-end framework.

**Requirements:**
- Component system with lifecycle
- Virtual DOM and diffing
- State management
- Event handling
- Routing
- Template syntax

**Learning Objectives:**
- Framework internals
- Rendering optimization
- System design

**Extension:** Add server-side rendering concept.

---

### Assignment E52: Build a Bundler
**Difficulty:** ⭐⭐⭐⭐⭐ (5/5) | **Time:** 150 mins

**Problem Statement:**
Build a simple module bundler.

**Requirements:**
- Parse ES6 imports/exports
- Build dependency graph
- Bundle into single file
- Handle circular dependencies
- Source maps concept

**Learning Objectives:**
- Module resolution
- AST parsing concept
- Bundling algorithms

**Extension:** Add code splitting.

---

### Assignment E53: Build a Test Framework
**Difficulty:** ⭐⭐⭐⭐⭐ (5/5) | **Time:** 120 mins

**Problem Statement:**
Build a testing framework.

**Requirements:**
- describe/it syntax
- Assertions library
- Mocking/spying
- Async test support
- Reporter system
- Watch mode

**Learning Objectives:**
- Test framework architecture
- Assertion design
- Test discovery

**Extension:** Add parallel test execution.

---

### Assignment E54: Build a State Machine
**Difficulty:** ⭐⭐⭐⭐ (4/5) | **Time:** 90 mins

**Problem Statement:**
Build XState-like state machine.

**Requirements:**
```javascript
const machine = createMachine({
  initial: 'idle',
  states: {
    idle: {
      on: { START: 'running' }
    },
    running: {
      on: { STOP: 'idle', PAUSE: 'paused' }
    },
    paused: {
      on: { RESUME: 'running', STOP: 'idle' }
    }
  }
});

const service = interpret(machine);
service.start();
service.send('START');
```

**Learning Objectives:**
- FSM implementation
- State transitions
- Guard conditions

**Extension:** Add hierarchical states.

---

### Assignment E55: Build GraphQL Client
**Difficulty:** ⭐⭐⭐⭐⭐ (5/5) | **Time:** 120 mins

**Problem Statement:**
Build a GraphQL client.

**Requirements:**
- Query execution
- Mutation support
- Variables handling
- Caching
- Subscriptions (concept)
- Error handling

**Learning Objectives:**
- GraphQL protocol
- Query parsing
- Cache management

**Extension:** Add optimistic updates.

---

### Assignment E56: Build Animation Engine
**Difficulty:** ⭐⭐⭐⭐⭐ (5/5) | **Time:** 120 mins

**Problem Statement:**
Build an animation library.

**Requirements:**
- Tween animations
- Easing functions
- Keyframe animations
- Chaining/sequencing
- Timeline control
- Performance optimization

**Learning Objectives:**
- Animation timing
- Easing mathematics
- RAF optimization

**Extension:** Add physics-based animations.

---

### Assignment E57: Build a CLI Parser
**Difficulty:** ⭐⭐⭐⭐ (4/5) | **Time:** 75 mins

**Problem Statement:**
Build a command-line argument parser.

**Requirements:**
```javascript
const cli = createCLI({
  name: 'mytool',
  version: '1.0.0',
  commands: {
    build: {
      description: 'Build the project',
      options: {
        watch: { alias: 'w', type: 'boolean' },
        output: { alias: 'o', type: 'string' }
      },
      action: (options) => { }
    }
  }
});

cli.parse(process.argv);
```

**Learning Objectives:**
- Argument parsing
- Option handling
- Help generation

**Extension:** Add interactive prompts.

---

### Assignment E58: Build ORM
**Difficulty:** ⭐⭐⭐⭐⭐ (5/5) | **Time:** 150 mins

**Problem Statement:**
Build a simple ORM.

**Requirements:**
```javascript
class User extends Model {
  static tableName = 'users';
  
  static fields = {
    id: { type: 'integer', primaryKey: true },
    name: { type: 'string' },
    email: { type: 'string', unique: true }
  };
  
  static relations = {
    posts: { type: 'hasMany', model: 'Post' }
  };
}

await User.create({ name: 'John', email: 'john@example.com' });
const users = await User.where({ active: true }).limit(10).get();
```

**Learning Objectives:**
- ORM patterns
- Query building
- Relationship handling

**Extension:** Add migrations.

---

### Assignment E59: Build Real-time Engine
**Difficulty:** ⭐⭐⭐⭐⭐ (5/5) | **Time:** 120 mins

**Problem Statement:**
Build real-time sync engine.

**Requirements:**
- WebSocket wrapper
- Room/channel concept
- Presence tracking
- Message acknowledgment
- Reconnection handling
- Conflict resolution (basic)

**Learning Objectives:**
- Real-time architecture
- Socket management
- State synchronization

**Extension:** Add CRDT basics.

---

### Assignment E60: Build Schema Validator
**Difficulty:** ⭐⭐⭐⭐ (4/5) | **Time:** 90 mins

**Problem Statement:**
Build Zod/Yup-like validator.

**Requirements:**
```javascript
const schema = z.object({
  name: z.string().min(1).max(100),
  email: z.string().email(),
  age: z.number().min(0).optional(),
  tags: z.array(z.string())
});

const result = schema.parse(data);
// or
const safeResult = schema.safeParse(data);
```

**Learning Objectives:**
- Schema validation
- Type coercion
- Error formatting

**Extension:** Add transform and refine.

---

### Assignment E61: Build Reactive System
**Difficulty:** ⭐⭐⭐⭐⭐ (5/5) | **Time:** 120 mins

**Problem Statement:**
Build Vue-like reactivity.

**Requirements:**
```javascript
const state = reactive({
  count: 0,
  doubled: computed(() => state.count * 2)
});

effect(() => {
  console.log(state.count, state.doubled);
});

state.count++; // Triggers effect
```

**Learning Objectives:**
- Proxy-based reactivity
- Dependency tracking
- Computed values

**Extension:** Add batch updates.

---

### Assignment E62: Build HTTP Router
**Difficulty:** ⭐⭐⭐⭐ (4/5) | **Time:** 75 mins

**Problem Statement:**
Build Express-like router.

**Requirements:**
```javascript
const router = createRouter();

router.get('/users', handler);
router.get('/users/:id', handler);
router.post('/users', handler);

router.use('/api', apiRouter);
router.use(authMiddleware);

// Pattern matching
router.match('GET', '/users/123');
// Returns { handler, params: { id: '123' } }
```

**Learning Objectives:**
- Route matching
- Parameter extraction
- Middleware integration

**Extension:** Add route groups.

---

### Assignment E63: Build Template Engine
**Difficulty:** ⭐⭐⭐⭐ (4/5) | **Time:** 90 mins

**Problem Statement:**
Build a template engine.

**Requirements:**
```javascript
const template = compile(`
  <h1>{{ title }}</h1>
  <ul>
    {% for item in items %}
      <li>{{ item.name }}</li>
    {% endfor %}
  </ul>
  {% if showFooter %}
    <footer>{{ footer }}</footer>
  {% endif %}
`);

const html = template({ title: 'List', items: [...] });
```

**Learning Objectives:**
- Template parsing
- Variable interpolation
- Control flow

**Extension:** Add partials and layouts.

---

### Assignment E64: Build Logger
**Difficulty:** ⭐⭐⭐ (3/5) | **Time:** 60 mins

**Problem Statement:**
Build a production logger.

**Requirements:**
```javascript
const logger = createLogger({
  level: 'info',
  transports: [
    new ConsoleTransport(),
    new FileTransport('app.log'),
    new HTTPTransport('https://logs.example.com')
  ],
  format: (entry) => { }
});

logger.info('Message', { context: 'data' });
logger.error('Error', error);

// Child logger
const childLogger = logger.child({ module: 'auth' });
```

**Learning Objectives:**
- Logging architecture
- Log levels
- Transport system

**Extension:** Add sampling and filtering.

---

### Assignment E65: Build Scheduler
**Difficulty:** ⭐⭐⭐⭐ (4/5) | **Time:** 75 mins

**Problem Statement:**
Build a task scheduler.

**Requirements:**
```javascript
const scheduler = createScheduler();

scheduler.every('5 minutes', () => { });
scheduler.cron('0 * * * *', () => { });  // Every hour
scheduler.once('2024-12-25 00:00:00', () => { });

scheduler.start();
scheduler.pause();
scheduler.resume();
scheduler.stop();

// Job management
scheduler.getJobs();
scheduler.cancelJob(jobId);
```

**Learning Objectives:**
- Cron parsing
- Job scheduling
- Timer management

**Extension:** Add job persistence.

---

### Assignment E66: Build Queue System
**Difficulty:** ⭐⭐⭐⭐ (4/5) | **Time:** 75 mins

**Problem Statement:**
Build a job queue.

**Requirements:**
```javascript
const queue = createQueue({
  concurrency: 5,
  retries: 3
});

queue.add({ type: 'email', data: { to: '...' } });
queue.process('email', async (job) => { });

queue.on('completed', (job) => { });
queue.on('failed', (job, error) => { });

// Priority
queue.add(job, { priority: 'high' });

// Delayed
queue.add(job, { delay: 60000 });
```

**Learning Objectives:**
- Queue patterns
- Retry strategies
- Concurrency control

**Extension:** Add dead letter queue.

---

### Assignment E67: Build Dependency Resolver
**Difficulty:** ⭐⭐⭐⭐⭐ (5/5) | **Time:** 90 mins

**Problem Statement:**
Build a dependency resolver.

**Requirements:**
```javascript
const resolver = createResolver();

resolver.register('a', [], () => 'A');
resolver.register('b', ['a'], (a) => `B(${a})`);
resolver.register('c', ['a', 'b'], (a, b) => `C(${a}, ${b})`);

resolver.resolve('c'); // C(A, B(A))

// Circular dependency detection
resolver.register('x', ['y'], () => {});
resolver.register('y', ['x'], () => {}); // Error
```

**Learning Objectives:**
- Dependency graphs
- Topological sort
- Cycle detection

**Extension:** Add lazy evaluation.

---

### Assignment E68: Build Data Grid
**Difficulty:** ⭐⭐⭐⭐⭐ (5/5) | **Time:** 150 mins

**Problem Statement:**
Build a production data grid.

**Requirements:**
- Virtual scrolling (100k+ rows)
- Column sorting
- Filtering
- Row selection
- Column resizing
- Inline editing
- Column pinning
- Export

**Learning Objectives:**
- Virtual rendering
- Large dataset handling
- Complex interactions

**Extension:** Add grouping and aggregation.

---

### Assignment E69: Build IDE Features
**Difficulty:** ⭐⭐⭐⭐⭐ (5/5) | **Time:** 180 mins

**Problem Statement:**
Build code editor features.

**Requirements:**
- Syntax highlighting
- Auto-indent
- Bracket matching/auto-close
- Multi-cursor (basic)
- Find and replace with regex
- Code folding
- Minimap

**Learning Objectives:**
- Text editing algorithms
- Syntax parsing
- Editor UX

**Extension:** Add autocomplete.

---

### Assignment E70: Full-Stack Application
**Difficulty:** ⭐⭐⭐⭐⭐ (5/5) | **Time:** 240 mins

**Problem Statement:**
Build a complete application.

**Requirements:**
Build a project management app with:
- Authentication system
- Real-time collaboration
- CRUD for projects/tasks
- Drag-and-drop kanban
- User permissions
- Activity timeline
- Notifications
- Search functionality

**Architecture:**
- Clean architecture
- Repository pattern
- Event-driven updates
- Optimistic UI
- Error boundaries
- Performance monitoring

**Learning Objectives:**
- System design
- Architecture patterns
- Production practices

**Extension:** Add offline support and PWA.

---

# 📋 CURRICULUM SUMMARY

## Total Assignments: 280

| Level | Assignments | Modules |
|-------|-------------|---------|
| 🟢 Beginner | B1-B70 (70) | Variables, Control Flow, Functions, Arrays/Objects, Projects |
| 🟡 Intermediate | I1-I70 (70) | DOM, Events, Async, Storage, Projects |
| 🟠 Advanced | A1-A70 (70) | ES6+, OOP, Browser APIs, Projects |
| 🔴 Expert | E1-E70 (70) | Design Patterns, Performance, Architecture, Capstones |

## Recommended Learning Path

1. **Foundation (4-6 weeks):** Complete Beginner Level
2. **Web Development (4-6 weeks):** Complete Intermediate Level
3. **Modern JavaScript (4-6 weeks):** Complete Advanced Level
4. **Professional Development (6-8 weeks):** Complete Expert Level

## Core Competencies Covered

### Beginner
- JavaScript syntax and fundamentals
- Control flow and loops
- Functions and scope
- Data structures basics

### Intermediate
- DOM manipulation
- Event handling
- Asynchronous programming
- Browser storage

### Advanced
- ES6+ features
- Object-oriented programming
- Browser APIs
- Application architecture

### Expert
- Design patterns
- Performance optimization
- Security best practices
- System design

---

**Congratulations on completing the JavaScript curriculum!**

