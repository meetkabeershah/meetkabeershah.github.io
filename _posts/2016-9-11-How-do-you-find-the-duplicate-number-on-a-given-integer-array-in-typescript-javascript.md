---
layout: post
title: How do you find the duplicate number on a given integer array in typescript/javascript?
---

This is one of the famous interview question of all times. 
> How do you find the duplicate number on a given integer array?

There are so many ways to solve it in many languages with many different approaches. The one I suggest in javascript/typescript is:

```
const findDuplicatesInAnArray = (inpArr) => {
  let sorted_arr = inpArr.slice().sort();
  let results = [];
  for (let i = 0; i < sorted_arr.length - 1; i++) {
    if (sorted_arr[i + 1] == sorted_arr[i]) {
      results.push(sorted_arr[i]);
    }
  }
  return results;
}

let duplicatedArray = [9, 9, 111, 2, 3, 4, 4, 5, 7];
console.log(`The duplicates in ${duplicatedArray} are ${findDuplicatesInAnArray(duplicatedArray)}`);
```