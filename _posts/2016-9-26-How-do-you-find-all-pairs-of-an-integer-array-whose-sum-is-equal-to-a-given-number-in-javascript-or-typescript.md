---
layout: post
title: How do you find all pairs of an integer array whose sum is equal to a given number in javascript or typescript
---

You must have seen this question in many of the interviews related to programming. This can be implemented in any language and using so many approaches. The solution I suggest is:

```
const findAllPairsOfAnIntegerArrayWhoseSumIsEqualToAGivenNumber = (arr, targetSum) => {
 const pairs = [];
  for(let i = 0; i< arr.length; i++) {
    for(let j = i+1;  j < arr.length; j++) {
      if(targetSum == arr[i] + arr[j]) {
          pairs.push([arr[i],arr[j]])
          console.log(`The sum of ${arr[i]} and ${arr[j]} is ${targetSum}`)
      }
    }
  }
 return pairs
}
```

And this is how you call it:

```
findAllPairsOfAnIntegerArrayWhoseSumIsEqualToAGivenNumber([0,1,2,3,4,5,6,7,8,9], 10)
```