+++
title = "Implement a loop that iterates through sorted array and sum any duplicate numbers then Also How to remove duplicates numbers."
date = "2023-04-13T10:33:46+02:00"
tags = ["JAVASCRIPT"]
categories = ["JAVASCRIPT"]
authors = ["Tejiri Mayone"]
banner = "/img/post/arrays-in-javaScript.png"
+++

## Introduction
The Array object, as with arrays in other programming languages, enables storing a collection of multiple items under a single variable name, and has members for performing common array operations.
|*[coped from developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)*|

First lets create an array to be used as an example. 

```
// Sample array of numbers
const numbers = [4, 2, 6, 1, 3, 2, 5, 4, 5, 7, 6];
```

Next, we will be using javascript built-in function to sort out array in ascending order

```
// Sort the array in ascending order
const sortedNumbers = numbers.sort((a, b) => a - b);
```

Then, we initialize a prev variable to keep track of the previously seen number and a sumOfDuplicates variable to keep track of the sum of duplicate numbers.

```
let prev = null;
let sumOfDuplicates = 0;
```

We then loop through the sorted array and check if the current number is equal to the previous number. If it is, we add the current number to the sumOfDuplicates. Otherwise, we update the prev variable to the current number.

Finally, we log the sumOfDuplicates to the console.

```
for (let i = 0; i < sortedNumbers.length; i++) {
    if (sortedNumbers[i] === prev) {
        sumOfDuplicates += sortedNumbers[i];
    }
    prev = sortedNumbers[i];
}

console.log(sumofDuplicates)
```
Below, is a complete code in this expample.

```
// Sample array of numbers
const numbers = [4, 2, 6, 1, 3, 2, 5, 4, 5, 7, 6];

// Sort the array in ascending order
const sortedNumbers = numbers.sort((a, b) => a - b);

//bonus to remove duplicates number, we will write it like so.
const uniqueNumber = [...new Set(numbers)]

let prev = null;
let sumOfDuplicates = 0;

for (let i = 0; i < sortedNumbers.length; i++) {
    if (sortedNumbers[i] === prev) {
        sumOfDuplicates += sortedNumbers[i];
    }
    prev = sortedNumbers[i];
}

console.log(sumOfDuplicates) // Output: 17
```
As a bonus to this code example I showed you how to remove duplicates from a number array.

```
const uniqueNumber = [...new Set(numbers)]
```

I hope this helps! Let me know if you have any questions.