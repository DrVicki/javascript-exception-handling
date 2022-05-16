## Overview

In this tutorial, you will learn how to handle exceptions.

## Introduction to JavaScript ```try…catch``` statement

The following example attempts to call the ```add()``` function that doesn’t exist:

```
let result = add(10, 20);
console.log(result);

console.log('Bye');
```

The JavaScript engine issues the following error:

```
Uncaught TypeError: add is not a function
```
The error message states the ```add``` is not a function and the error type is ```TypeError```.

When the JavaScript engine encounters an error, it issues the error and immediately terminates the execution of the entire script. In the above example, the code execution stops at the first line.

Sometimes, you want to handle the error and continue the execution. To do that, you use the ```try...catch``` statement with the following syntax:

```
try {
  // code may cause error
} catch(error){
  // code to handle error
}
```
In this syntax:

  - First, place the code which may cause an error in the ```try``` block.
  - Second, implement the logic to handle the error in the ```catch``` block.

If an error occurs in the ```try``` block, the JavaScript engine immediately executes the code in the ```catch``` block. Also, the JavaScript engine provides you with an error object which contains detailed information about the error.

Basically, the error object has at least two properties:

  1. ```name``` specifies the error name.
  2. ```message``` explains the error in detail.

If no error occurs in the ```try``` block, the JavaScript engine ignores the ```catch``` block.

> Note that web browsers may add more properties to the error object. For example, Firefox adds ```filename```, ```lineNumber```, and ```stack``` properties to the error object.

It’s a good practice to place only the code which may cause an exception in the ```try``` block.

The following flowchart illustrates how the ```try...catch``` statement works:
![image](https://user-images.githubusercontent.com/47826697/168500816-845dde72-deb8-4cb7-97b1-c9e5e46e23f2.png)

## JavaScript ```try…catch``` statement examples

The following example uses the ```try...catch``` statement to handle the error:

```
try {
  let result = add(10, 20);
  console.log(result);
} catch (e) {
  console.log({ name: e.name, message: e.message });
}
console.log('Bye');
```
**Output**

```
{name: 'TypeError', message: 'add is not a function'}
Bye
```
In this example, we call the ```add()``` function and assign the ```return``` value to the result variable. Because the ```add()``` function doesn’t exist, the JavaScript engine skips the statement which outputs the result to the console:

```
console.log(result);
```
It immediately executes the statement in the ```catch``` block which outputs the error name and message:

```
console.log({ name: e.name, message: e.message });
```
Since we already handled the error, the JavaScript engine continues to execute the last statement:

```
console.log('Bye');
```
## Ingoring the ```catch``` block

The following example defines the ```add()``` function which returns the sum of two arguments:

```
const add = (x, y) => x + y;

try {
  let result = add(10, 20);
  console.log(result);
} catch (e) {
  console.log({ name: e.name, message: e.message });
}
console.log('Bye');
```
**Output**:

```
30
Bye
```
In this example, no error occurs because the ```add()``` function exists. Therefore, the JavaScript engine skips the ```catch``` block.

## The exception identifier

When an exception occurs in the ```try``` block, the exception variable (```e```) in the catch block store the exception object.

If you don’t want to use the exception variable, you can omit it like this:

```
try {
  //...
} catch {
  //...
}
```
For example, the following uses the ```try…catch``` statement without the exception variable:

```
const isValidJSON = (str) => {
  try {
    JSON.parse(str);
    return true;
  } catch {
    return false;
  }
};

let valid = isValidJSON(`{"language":"JavaScript"}`);
console.log(valid);
```
**How it works**.

  - First, define the ```isValidJSON()``` function that accepts a string and returns ```true``` if the string is a valid JSON or ```false``` otherwise.
    - To validate JSON, the ```isValidJSON()``` function uses the ```JSON.parse()``` method and ```try...catch``` statement.
    - The ```JSON.parse()``` method parses a JSON string and returns an object. If the input string is not valid JSON, the ```JSON.parse()``` throws an exception.
    - If no exception occurs, the function returns ```true``` in the ```try``` block. Otherwise, it returns ```false``` in the ```catch``` block.
  - Second, call the ```isValidJSON()``` function and pass a JSON string into it:
```
let valid = isValidJSON(`{"language":"JavaScript"}`);
```
   - Since the input string is valid JSON format, the function returns true.

  - Third, output the result to the console:

```
console.log(valid);
```
### Summary

Use the ```try...catch``` statement to handle exceptions in JavaScript.
Place only the code which may cause an exception in the ```try``` block.


# JavaScript ```throw``` exception

in this tutorial, you’ll learn how to use the JavaScript ```throw``` statement to throw an exception.

## Introduction to the JavaScript ```throw``` statement

The ```throw``` statement allows you to throw an exception. Here’s the syntax of the ```throw``` statement:

```
throw expression;
```
In this syntax, the expression specifies the value of the exception. Typically, you’ll use a new instance of the Error class or its subclasses.

When encountering the ```throw``` statement, the JavaScript engine stops executing and passes the control to the first ```catch``` block in the call stack. If no catch block exists, the JavaScript engine terminates the script.

**JavaScript throw exception examples**

Let’s take some examples of using the ```throw``` statement.

  1. Using the JavaScript ```throw``` statement to throw an exception
    - The following example uses the ```throw``` statement to throw an exception in a function:
```
function add(x, y) {
  if (typeof x !== 'number') {
    throw 'The first argument must be a number';
  }
  if (typeof y !== 'number') {
    throw 'The second argument must be a number';
  }

  return x + y;
}

const result = add('a', 10);
console.log(result);
```
How it works.

First, define the ```add()``` function that accepts two arguments and returns the sum of them. The ```add()``` function uses the ```typeof``` operator to check the type of each argument and throws an exception if the type is not number.

Second, call the ```add()``` function and pass a string and a number into it.

Third, show the result to the console.

The script causes an error because the first argument ("```a```") is not a number:

```
Uncaught The first argument must be a number
```
To handle the exception, you can use the ```try...catch``` statement. For example:

```
function add(x, y) {
  if (typeof x !== 'number') {
    throw 'The first argument must be a number';
  }
  if (typeof y !== 'number') {
    throw 'The second argument must be a number';
  }

  return x + y;
}

try {
  const result = add('a', 10);
  console.log(result);
} catch (e) {
  console.log(e);
}
```
**Output**:
```
The first argument must be a number
```
In this example, we place the call to the ```add()``` function in a ```try``` block. Because the expression in the throw statement is a string, the exception in the ```catch``` block is a string as shown in the output.

  2. Using JavaScript throw statement to throw an instance of the Error class

  In the following example, we throw an instance of the Error class rather than a string in the   ```add()``` function;

```
function add(x, y) {
  if (typeof x !== 'number') {
    throw new Error('The first argument must be a number');
  }
  if (typeof y !== 'number') {
    throw new Error('The second argument must be a number');
  }

  return x + y;
}

try {
  const result = add('a', 10);
  console.log(result);
} catch (e) {
  console.log(e.name, ':', e.message);
}
```
**Output**:

```
Error : The first argument must be a number
```
As shown in the output, the exception object in the ```catch``` block has the ```name``` as Error and the ```message``` as the one that we pass to the ```Error()``` constructor.

  3. Using JavaScript throw statement to throw a user-defined exception

  Sometimes, you want to throw a custom error rather than the built-in Error. To do that, you     can define a custom error class that extends the Error class and throw a new instance of that   class. For example:

First, define the ```NumberError``` that extends the Error class:

```
class NumberError extends Error {
  constructor(value) {
    super(`"${value}" is not a valid number`);
    this.name = 'InvalidNumber';
  }
}
```
The ```constructor()``` of the ```NumberError``` class accepts a value you’ll pass into it when creating a new instance of the class.

In the ```constructor()``` of the ```NunberError``` class, we call the constructor of the Error class via the ```super``` and pass a string to it. Also, we override the name of the error to the literal string ```NumberError```. If we don’t do this, the name of the ```NumberError``` will be ```Error```.

Second, use the ```NumberError``` class in the ```add()``` function:

```
function add(x, y) {
  if (typeof x !== 'number') {
    throw new NumberError(x);
  }
  if (typeof y !== 'number') {
    throw new NumberError(y);
  }

  return x + y;
}
```
In the ```add()``` function, we throw an instance of the ```NumberError``` class if the argument is not a valid number.

Third, catch the exception thrown by the ```add()``` function:

```
try {
  const result = add('a', 10);
  console.log(result);
} catch (e) {
  console.log(e.name, ':', e.message);
}
```
**Output**:
```
NumberError : "a" is not a valid number
```
In this example, the exception ```name``` is ```NumberError``` and the ```message``` is the one we pass into the ```super()``` in the ```constructor()``` of the ```NumberError``` class.

### Summary

Use the JavaScript ```throw``` statement to throw a user-defined exception.
