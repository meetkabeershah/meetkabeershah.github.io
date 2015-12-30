---
layout: post
title: C# code documentation
---

![Documentation please](http://www.webpal.net/blog/wp-content/uploads/2011/11/clutter_cartoon_3.png)

[courtesy](http://www.webpal.net/blog/tag/document-management-2/)

The golden rule of code documentation:

> Try to document [why](http://stackoverflow.com/a/4929769) (code design decisions) and avoid what (code design descriptions).

To keep up with the increasing complexity of the project, it's very important to document the coding decisions. It's one of the best practices.

[Visual studio](https://www.visualstudio.com/) provides some elegant ways for code documentation to keep the code understandable. It can also understand the changes that one make on hard code.

#Single or multi line comments

 - Short (or long) functional descriptions

	<xmp>
	//single line comment
	</xmp>

These are necessary to describe functionality in little.

	<xmp>
	/*
	multiple
	line
	comments
	*/
	</xmp>

Avoid them. It is advisable to avoid writing essays about code. The end product shall be code not their long descriptions.

#Collapsible regions

 - Summary of the functional block

	<xmp>
	#region Some code block

	//some code here
    	//some foo bar
    	//Fizz Buzz
    	//some unicorns
    
	#endregion
    
	<xmp>

Regions are collapsible. Just hover over the collapsed region and get a glance.

![Glance in collapsed code](http://imgur.com/wsEL9yo)

[courtesy](http://imgur.com/)

#Summary

 - Summary of the function or property

        /// <summary>
        /// Summary description for the function or property goes here
        /// </summary>

![summary method description](http://imgur.com/ksUWv5O)

[courtesy](http://imgur.com/)

 - Summary of the function parameter

        /// <param name="TestParameter">Summary description for the parameter goes here</param>

![parameter desc](http://imgur.com/zwKtSLt)

[courtesy](http://imgur.com/)

Visual studio changes this section after change of the parameter name.

![Change of parameters](http://imgur.com/5RWuBMJ)

[courtesy](http://imgur.com/)

 - Summary of the returning stuff

	`///<returns>Summary description for the function result goes here</returns>`

A simple example:

    /// <summary>
    /// Main class of the project
    /// </summary>
    class Program
    {
        /// <summary>
        /// Main entry point of the program
        /// </summary>
        /// <param name="args">Command line args</param>
        static void Main(string[] args)
        {
            //Do stuff
        }
    }
