---
layout: post
title: How do you find the largest and smallest number for an unsorted integer array in typescript/javascript?
---

One of the most famous interview questions is:

> How do you find the largest and smallest number for an unsorted integer array?

This question relates to data structures. Hence can be implemented using any language or approach. I suggest the javascript/typescript implementation as this:

```
const numbers = [2, 40, 9, 21, 1, 16, 24];

const smallest = Math.min(...numbers);
const largest = Math.max(...numbers);

console.log('Smallest Value:', smallest); // Smallest Value: 1
console.log('Largest Value:', largest);   // Largest Value: 40
```
