---
layout: post
title: Javascript Tip - Use Optional Chaining
---

Sometimes we need to check the existence / truthiness of properties on objects / classes. For example, this is how we generally write it:

<pre>
<code>
if (family && family.mother && family.mother.child){
     console.log(family.mother.child);
}
</code>
</pre>


This can be written in short link this:

`console.log(family?.mother?.child);`

The magical operator being used here i.e. `?.` is called Optional chaining operator. Use it to shortify your code base.

Read more: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Optional_chaining