---
layout: post
title: Binding in Javascript example!
---

![Javascript Binding in English simplified!](https://codersblock.com/static/javascript-function-methods-bind-545d7331791004779fee88d94c3494cc.png)

[credit](https://codersblock.com/blog/javascript-function-methods-bind/)

To attach an object to the scope & context of a function the function bind is used. The attachment of the scope & context is called as binding.

Here is an example:

<pre>
<code>
let object1 = {x:1, y:2};
let object2 = {x:10, y:20};

function printThis(){
    // the bound object is referenced using the this keyword
    console.log(this);
}

// bind an object to a function
let bindprintThis_To_object1 = printThis.bind(object1);

let bindprintThis_To_object2 = printThis.bind(object2);

bindprintThis_To_object1() // {x:1, y:2}
bindprintThis_To_object2() // {x:10, y:20}
</code>
</pre>

The context `this` will change depending on what is `bind` to `printThis`. 