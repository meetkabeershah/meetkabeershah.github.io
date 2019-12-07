---
layout: post
title: How do you find the missing number in a given integer array of 1 to 10 in typescript or javascript?
---

One of the most famous interview question is 

> How do you find the missing number in a given integer array of 1 to 10?

There are so many ways to solve it! Since, I work on typescript or javascript - I have formulized this solution:

```
var a = [1,2,3,5,6,8,9,10],
  count = a.length;
var missing = new Array();

for (var i = 1; i <= count; i++) {
  if (a.indexOf(i) == -1) {
    missing.push(i);
  }
}
console.log(missing); // to check the result.
```

Hope this helps!
