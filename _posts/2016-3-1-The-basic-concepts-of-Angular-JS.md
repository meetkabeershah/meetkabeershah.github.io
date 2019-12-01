---
layout: post
title: The basic concepts of Angular JS
---

![Angular JS by Google](https://d1067y8t86k9le.cloudfront.net/wp-content/uploads/2016/04/22150642/angular_js.jpg)

[courtesy](https://www.amitavroy.com/justread/content/articles/working-xml-angular-js/)

# Why should we use Angular JS?

 - Helps organize the javascript code
 - Helps create responsive (as in fast) websites
 - Plays well with jQuery
 - Is easy to test

# What is Angular JS?
 
> A client side javascript framework for adding interactivity to HTML.

We need to figure out when to trigger our Javascript.

# Directives

> A directive is a marker on a HTML tag that tells Angular to run or reference some Javascript code.

e.g. In the following code snippet, `ng-crontroller` is a **marker** on body tag 

    <body ng-crontroller='abcController'>
    </body>

And the referenced javascript code is:

    function abcController(){
     alert('hello Angular JS!');
    }


The first step is to download the library from the [official website](https://angularjs.org)


# Modules

 - Modules are where we write pieces of our Angular application to keep our code encapsulated to make our code more maintainable, testable and readable.
 - Modules are where we define depencies for our application.

![Module dependencies](https://lh3.googleusercontent.com/n2g4PqKfllLyrdlTbXv_4mtSPrXv0p2bzwlirBofVwG5shLptExjrrnn9BP3QdUky-bIiKCGiyjBZN5OZWmeBvMgjUWzxGXp0_NzXWlPOI5Fjn7m18P6iJs2reLZZ8jSJTJaLqycjhxRCtFKl2VLDsT5N7rqw028H2XH7ZwAslSM85-VXGPiXwYalJR9aecT7YoGSjORixSKsBdewOV09l-yx-YkI-IJoV62UMaoclnDoLrr8WkJHuWn3bW24krJCxenhmK5QiCVWcVhEPxj1EZ-mLKZ6K_EqJ26py3FD2NAr0YT-Kad4HrFYYwDrxbOEU8VYozi_FcjXLRdKB3teN-8a3hIbCXAHengCYJ8TnLYeXu53P4FAHoarOJFSX7J4MM9mWulYZrwUOqz6LccoJUHm-txtqpWe79k4ht25ScnX89PCmmXraLYtdkCjKXc1eCZliIe5KwWkINznaY-cddX663tONMGRYGOnEJVzpkEDGm9fjUFwkVUWoYkI11fGSuBiDwLiHOTQjAs8ldVE4cWXr5-PHw4VcfQtWFxrxJQHB_MCZB5-U-mvJuLUSH6C-Z-olczanmekrg7jGH0tC0ugSJZmJrXXobnYhbb-m-wOviSwuAs=w188-h177-no)

Let's create a module:

    var app = angular.module('abcApp',[]);

And use it:

    <html ng-app='abcApp'>
    </html>

The above code does nothing as such, currently it is just saying that the entire `HTML` area is part of the Angular application. We can start using expressions at this point:

{{ 4 + 6 }}

Expressions can also be used for string manipulation:

{{ 'Hello ' + 'AngularJS' }}


# Controllers

> Controllers are where we define our app's behavior by defining functions and values.

Let's have some data printed on the view using controller.

    (function(){

	var app = angular.module('abc', []);
	app.controller('abcController', function(){	
	this.a = abc;
	});
	
	var abc = {
	propertyA : 'A',
	propertyB: 'B'
	};
    })();

The view should look like this:

    <div ng-controller='abcController as abc' >
      {{abc.a.propertyA}}
      {{abc.a.propertyB}}
    </div>

This works well with a single object but what if we have an array?

Inside a controller:

    (function(){

	var app = angular.module('abc', []);
	app.controller('abcController', function(){	
	this.as = abc;
	});
	
	var abc = [{
	propertyA : 'A',
	propertyB: 'B'
	}, {
	propertyA : 'C',
	propertyB: 'D'
	}, {
	propertyA : 'E',
	propertyB: 'F'
	}];
    })();

To show this in the view, we need to use `ng-repeat`:

    <div ng-controller='abcController as abc' >
      <div ng-repeat='a in abc.as'>
      {{a.propertyA}}
      {{a.propertyB}}
      </div>
    </div>

There are a lot of [build in directives](http://www.techstrikers.com/AngularJS/angularjs-built-in-directives.php) like `ng-app`, `ng-controller`, `ng-show`, `ng-hide`, `ng-repeat` etc. 

# Filters

The basic formula of filters is as follows:

    {{ data* | filter: options*}}

e.g.:


    {{ '1388123412323' | date: 'MM/dd/yyyy @ h:mm' }} <!-- formats the date -->
    {{ 'lowercase string' | uppercase }} <!-- uppercases the string -->
    {{ 'a vvveeeerrrryy llooonnngggg strrrriiiinngggg' | limitTo: 8 }} <!-- limits the string to specified number 8 -->	
    <li ng-repeat='a in abcs | limitTo: 3'> <!-- limits the array elements to specified number 3 -->
    <li ng-repeat='a in abcs | orderBy: -A'> <!-- sorts the array elements in descending order because of - charachter -->

The pipe charachter in the expression asks the expression to take the first parameter to the expression and pass it to the second part of the expression. Like in the following:

    {{ '$2.695865' | currency }}

Currency is a filter in this case.

[source](https://www.codeschool.com/courses/shaping-up-with-angularjs)