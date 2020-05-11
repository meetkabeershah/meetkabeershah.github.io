---
layout: post
title: Closures in Javascript simplified!
---

![Javascript Closures in English simplified!](https://www.debuggr.io/static/deed0850c5939ca6f2e263e03e0a9249/ba299/cover.png)

[credit](https://www.debuggr.io/js-closure-in-depth/)

A closure is a feature in JavaScript where an inner function has access to the outer (enclosing) function's variables!

Here is an example of a very uncommon closure in javascript:

<pre>
<code>
const name = 'Mohammad Ali';

function innerFunction(){
    console.log(name);
}

innerFunction();
</code>
</pre>

The function `innerFunction()` has access to the variable `name`. The outer scope of the file in which the code resides, while there is no explicit function declaration - the function `innerFunction()` having access to a variable `name` satisfies the condition of a inner function having access to an outer scope variable.

<pre>
<code>
function outerBodyFunction() {
    const name = 'Mohammad Ali';

    function innerFunction(){
        console.log(name);
    }

    return innerFunction;
}

let _innerFunction = outerBodyFunction(); // or outerBodyFunction()();
_innerFunction();
</code>
</pre>

The function `innerFunction()` has access to the variable `name`. The outer scope of the `outerBodyFunction` function in which the code resides, the function `innerFunction()` having access to a variable `name` satisfies the condition of a inner function having access to an outer scope variable.
