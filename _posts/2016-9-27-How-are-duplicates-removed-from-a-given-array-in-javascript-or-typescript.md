---
layout: post
title: How are duplicates removed from a given array in javascript or typescript
---

If you have an array which contains duplicate values and you wish to remove the duplicates - in other words if you want distinct values in your array - then `Set` comes to the rescue.

Here is an example:

```
let nonUniqueArray = [1, 1, 2, 3, 4, 5];

console.log(`Original array : ${nonUniqueArray}`);

let uniqueArray = [...new Set(nonUniqueArray)];

console.log(`Unique array : ${uniqueArray}`);
```

Hope this helps!