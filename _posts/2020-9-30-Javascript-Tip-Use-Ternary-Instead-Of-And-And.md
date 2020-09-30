---
layout: post
title: Javascript tip - Use ternaries rather than && in JSX
---

When JavaScript evaluates 0 && anything the result will always be 0 because 0 is falsy, so it doesn't evaluate the right side of the &&

<pre>
<code>
console.log(0 && true) // 0 - falsy, right side not evaluated
console.log(0 && false) // 0 - falsy, right side not evaluated
console.log(false && true) // falsy, right side not evaluated
console.log(false && false) // falsy, right side not evaluated
</code>
</pre>

Look at these too:

<pre>
<code>
console.log(1 && true) // true, right side evaluated
console.log(1 && false) // false, right side evaluated
console.log(1 && false) // false, right side evaluated
console.log(1 && false) // false, right side evaluated
</code>
</pre>

The solution? Use a ternary to be explicit about what you want rendered in the falsy case

Read more: [https://kentcdodds.com/blog/use-ternaries-rather-than-and-and-in-jsx](https://kentcdodds.com/blog/use-ternaries-rather-than-and-and-in-jsx)