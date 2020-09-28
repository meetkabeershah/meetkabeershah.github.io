---
layout: post
title: Javascript best practices - Shortify falsy / truthy checks
---

Sometimes we need to assign only truthy (not undefined/null/empty) values to our variables.

It is done like this:

<pre>
<code>
if (myVar !== null && myVar !== 'undefined' && myVar !== '') {
   yourVar = myVar;
}
else {
  yourVar = 'new default value';
}
</code>
</pre>

This can be optimized as:


`yourVar = myVar || 'new default value';`