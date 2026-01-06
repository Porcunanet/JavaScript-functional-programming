# JavaScript Functional Programming Code Snippets

## Check to see if a number is even or odd

```javascript
const checkEven = n => n % 2 ===0 ? "even":"odd";
```

## Adds number of odd numbers based on user input
```
const numOfOdds = (num) => {
    return Math.floor((num + 1) / 2);
    }
```
## FUNCTIONAL PROGRAMMING IN JAVASCRIPT

### Sample data to work with
```
const numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
const users = [
  { id: 1, name: 'Alice', age: 28, department: 'Engineering' },
  { id: 2, name: 'Bob', age: 35, department: 'Sales' },
  { id: 3, name: 'Charlie', age: 22, department: 'Engineering' },
  { id: 4, name: 'Diana', age: 30, department: 'Marketing' },
  { id: 5, name: 'Eve', age: 26, department: 'Engineering' }
];
```

## 1. MAP - Transform each element
```
console.log('Transforms each element in an array using a function');

// Double each number
const doubled = numbers.map(n => n * 2);
console.log('numbers.map(n => n * 2):', doubled);
// [2, 4, 6, 8, 10, 12, 14, 16, 18, 20]

// Extract user names
const names = users.map(user => user.name);
console.log('users.map(user => user.name):', names);
// ['Alice', 'Bob', 'Charlie', 'Diana', 'Eve']

// Extract and transform multiple properties
const userSummaries = users.map(user => ({
  name: user.name,
  info: `${user.name} is ${user.age} years old`
}));
console.log('Transform with objects:', userSummaries);
```

## 2. FILTER - Select elements that meet criteria
```
console.log('\n--- FILTER ---');
console.log('Returns a new array with elements that pass the test');

// Get even numbers
const evenNumbers = numbers.filter(n => n % 2 === 0);
console.log('numbers.filter(n => n % 2 === 0):', evenNumbers);
// [2, 4, 6, 8, 10]

// Get users from Engineering department
const engineers = users.filter(user => user.department === 'Engineering');
console.log('engineers:', engineers);

// Get users over 25
const seniorUsers = users.filter(user => user.age > 25);
console.log('users over 25:', seniorUsers.map(u => u.name));
```

## 3. REDUCE - Combine elements into single value
```
console.log('\n--- REDUCE ---');
console.log('Reduces array to a single value by applying a function');

// Sum all numbers
const sum = numbers.reduce((accumulator, current) => accumulator + current, 0);
console.log('Sum of numbers:', sum);
// 55

// Product of numbers
const product = numbers.reduce((acc, curr) => acc * curr, 1);
console.log('Product of numbers:', product);

// Count occurrences (group by)
const departments = users.reduce((acc, user) => {
  if (!acc[user.department]) {
    acc[user.department] = [];
  }
  acc[user.department].push(user.name);
  return acc;
}, {});
console.log('Users by department:', departments);
// { Engineering: [...], Sales: [...], Marketing: [...] }

// Build a single object from array
const userMap = users.reduce((acc, user) => {
  acc[user.id] = user;
  return acc;
}, {});
console.log('User map by ID:', userMap);
```

## 4. FIND - Get first matching element
```
console.log('\n--- FIND ---');
console.log('Returns the first element that passes the test');

// Find first number greater than 5
const firstGreaterThan5 = numbers.find(n => n > 5);
console.log('First number > 5:', firstGreaterThan5);
// 6

// Find user named 'Bob'
const bob = users.find(user => user.name === 'Bob');
console.log('Found user:', bob);
```

## 5. SOME - Check if any element matches
```
console.log('\n--- SOME ---');
console.log('Returns true if at least one element passes the test');

// Check if any number is greater than 8
const hasNumberGreaterThan8 = numbers.some(n => n > 8);
console.log('Has number > 8:', hasNumberGreaterThan8);
// true

// Check if any user is 40+ years old
const hasOlderUser = users.some(user => user.age >= 40);
console.log('Has user 40+:', hasOlderUser);
// false
```

## 6. EVERY - Check if all elements match
```
console.log('\n--- EVERY ---');
console.log('Returns true if all elements pass the test');

// Check if all numbers are positive
const allPositive = numbers.every(n => n > 0);
console.log('All numbers positive:', allPositive);
// true

// Check if all users are adults (18+)
const allAdults = users.every(user => user.age >= 18);
console.log('All users are adults:', allAdults);
// true
```

## 7. FOREACH - Execute function for each element
```
console.log('\n--- FOREACH ---');
console.log('Executes a function for each element (side effects)');

console.log('Numbers (forEach):');
numbers.forEach((n, index) => {
  if (index < 3) console.log(`  Index ${index}: ${n}`);
});
```

## COMBINING METHODS (CHAINING & COMPOSITION)
```
console.log('\n--- CHAINING & COMPOSITION ---');

// Complex example: Filter engineers, map to names, and join
const engineerNames = users
  .filter(user => user.department === 'Engineering')
  .map(user => user.name)
  .join(', ');
console.log('Engineer names:', engineerNames);
// 'Alice, Charlie, Eve'

// Complex example: Get total age of all users over 25
const totalAgeOver25 = users
  .filter(user => user.age > 25)
  .map(user => user.age)
  .reduce((sum, age) => sum + age, 0);
console.log('Total age of users over 25:', totalAgeOver25);

// Complex example: Transform and flatten
const userInfo = users
  .filter(user => user.age >= 25)
  .map(user => ({
    ...user,
    ageGroup: user.age < 30 ? '25-29' : '30+'
  }))
  .sort((a, b) => a.age - b.age);
console.log('Filtered and transformed users:', userInfo);
```

## PRACTICAL EXAMPLES
```
console.log('\n--- PRACTICAL EXAMPLES ---');

// Example 1: Calculate statistics
const stats = {
  average: numbers.reduce((sum, n) => sum + n, 0) / numbers.length,
  max: Math.max(...numbers),
  min: Math.min(...numbers)
};
console.log('Statistics:', stats);

// Example 2: Data transformation for API
const apiPayload = users
  .filter(user => user.department === 'Engineering')
  .map(user => ({
    id: user.id,
    display_name: user.name.toUpperCase(),
    category: user.department
  }));
console.log('API payload:', apiPayload);

// Example 3: Check data validity
const hasInvalidUsers = users.some(user => !user.name || user.age < 0);
console.log('Has invalid users:', hasInvalidUsers);

// Example 4: Create frequency map
const numberFrequency = [1, 2, 2, 3, 3, 3, 4, 4, 4, 4].reduce((acc, num) => {
  acc[num] = (acc[num] || 0) + 1;
  return acc;
}, {});
console.log('Number frequency:', numberFrequency);
// { 1: 1, 2: 2, 3: 3, 4: 4 }
```

## COMPOSING FUNCTIONS
```
console.log('\n--- FUNCTION COMPOSITION ---');

// Create reusable filter functions
const isEven = n => n % 2 === 0;
const isGreaterThan5 = n => n > 5;
const double = n => n * 2;

// Use them together
const result = numbers
  .filter(isEven)
  .filter(isGreaterThan5)
  .map(double);
console.log('Even numbers > 5, doubled:', result);
// [12, 16, 20]

// Compose functions
const compose = (...fns) => value => fns.reduceRight((v, fn) => fn(v), value);
const pipeline = (...fns) => value => fns.reduce((v, fn) => fn(v), value);

const addTen = x => x + 10;
const multiplyByTwo = x => x * 2;
const subtract5 = x => x - 5;

const pipedFunction = pipeline(addTen, multiplyByTwo, subtract5);
console.log('Pipeline result (10 + 10) * 2 - 5 =', pipedFunction(10));
// 35
```

## KEY DIFFERENCES & WHEN TO USE
```
console.log('\n--- WHEN TO USE EACH METHOD ---');
console.log(`
MAP      - Transform data (1 input → 1 output)
FILTER   - Select subset of data based on criteria
REDUCE   - Combine data into single value (aggregation)
FIND     - Get first matching element (short-circuits)
SOME     - Check if ANY element matches (short-circuits)
EVERY    - Check if ALL elements match (short-circuits)
FOREACH  - Execute side effects, no return value
`);
```
