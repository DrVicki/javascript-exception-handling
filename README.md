## Overview

In this tutorial, you will learn how to use the JavaScript try...catch statement to handle exceptions.

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
