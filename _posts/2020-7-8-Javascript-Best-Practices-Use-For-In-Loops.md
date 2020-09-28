---
layout: post
title: Javascript Best Practices - Use For In Loops
---

For loops can be shortened and cleaned. Let's see an example:

Long form:

<pre>
<code>
const friends = ['amar', 'akbar', 'anthony'];
for (let i = 0; i < friends.length; i++){
 console.log(friends[i]);
}
</code>
</pre>

Short / clean form:

<pre>
<code>
const friends = ['amar', 'akbar', 'anthony'];
for (const friend in friends){
 console.log(friend);
}
</code>
</pre>

[https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...in](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...in)