# Path to Clean Code

Mentioned below are some day to day code snippets that you may write or encounter while development, along with the best practices that we should follow and bad practices to avoid.

### Variable declaration

```bash
//Bad Practice
let a = 32;
var x = 'Ravi';
const q = [ { name: 'Ravi', age: 21 }, { name: 'Mahima', age: 26 } ]

//Good Practice
let age = 32;
var name = 'Ravi';
const users = [ { name: 'Ravi', age: 21 }, { name: 'Mahima', age: 26 } ]
```
A variable name should always be meaningful and relevant to the data that is being assigned to it.


### Arrow Functions

```bash
//Bad Practice
<ChildComponent 
  incrementCounter={() => setCounter(counter+1))}
/>

//Good Practice
const incrementCounter = () => {
  setCounter(counter+1);
}

<ChildComponent 
  incrementCounter={incrementCounter}
/>
```
We should avoid direct function call while passing a function as prop to child component.

```bash

const incrementCounter = () => {
  setCounter(counter+1);
}

...
//Bad Practice
<ChildComponent 
  incrementCounter={() => incrementCounter()}
/>

//Good Practice
<ChildComponent 
  incrementCounter={incrementCounter}
/>
```
While passing a function to child component we should not write another arrow function to call the previous function as when to parent component re-render it will bind the function to child on each render. 


### Functions

```bash
//Bad Practice
const setUsername = (username) => {
    const name = username || 'Test';
    ...
}

//Good Practice
const setUsername = (username = 'Test') => {
    ...
}
```
When you write a function that can be called without any parameter in it and you want to assign a default value to the parameter, instead of short circuiting or conditionals one should use Default value.

```bash
//Bad Practice
const createUser = (name, age, gender, dob, salary) => {
  ...
}

createUser('Ravi', 21, 'Male', '20-11-1990', 200000);

//Good Practice
const createUser = ({name, age, gender, dob, salary}) => {
  ...
}

createUser({
  name: 'Ravi', 
  age: 21, 
  gender: 'Male', 
  dob: '20-11-1990', 
  salary: 200000
});
```
While calling a function that take multiple parameters one should create and call function using Objects as JavaScript allow you to create objects on the fly, plus it improves your code visibility to other.

```bash
//Bad Practice
const setUser = () => {
  const salary = hra + da + ctc;
  ...
}

const setClient = () => {
  const salary = hra + da + ctc;
  ...
}

//Good Practice
const calculateSalary = (hra, da, ctc) => {
  return hra + da + ctc;
}

const setUser = () => {
  const salary = calculateSalary(hra, da, ctc);
  ...
}

const setClient = () => {
  const salary = calculateSalary(hra, da, ctc);
  ...
}
```
While making a heavy computation logic in multiple functions separately, we should write a separate function to cater to that logic. This will eventually break down the code in small pieces of logic and more readable.


### Template Literals

```bash
//Bad Practice
const lastName = 'Peters';
const fullName = 'Russell ' + lastname

//Good Practice
const lastName = 'Peters';
const fullName = `Russell ${lastname}`
```
Template literals help create multi-line strings and perform string interpolation.


### Conditionals

```bash
//Bad Practice
if(status == 'FETCHED' || status == 'FETCHING' || status == 'UPDATING' || status == 'UPDATED'){
  ...
}

//Good Practice
const checkCondition = (status) => {
  return ['FETCHED', 'FECTHING', 'UPDATING' , 'UPDATED'].includes(status);
}

if(checkCondition()){
  ...
}
```
Instead of chaining multiple condition we can club them in a function and write the logic withing the function, so that we can use it at multiple places.  


### Error Handling

```bash
//Bad Practice
const getUserName = async() => {
  await getUserApi(); // this code can break 
}

//Good Practice
const getUserName = async() => {
  try {
    await getUserApi();
  } catch (e) {
    //handle errors
  } 
} 
```
Handling errors in your code is very important one should always wrap a piece of code inside try catch if it is making heavy computation or prone to error. 


### Async Await

```bash
//Bad Practice
const getUser = () => {
  getFromApi.then(res => {
    ...
  }).catch(e => {
    ...
  });
}

//Good Practice
const getUser = async() => {
  try {
    const data = await getFromApi();
    ...
  } catch(e) {
    ...  
  }
}
```
Rather than using then catch and landing in a callback hell one should use async await along with try catch.
