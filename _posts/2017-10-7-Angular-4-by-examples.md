---
layout: post
title: Angular 4 by examples
---

![Plunkr + Angular](http://terumi.me/blogs/meandev/Plunker-and-AngularJS.png)

[courtesy](http://mean.ghost.io/sandbox-eval-plunker-and-angularjs/)

The best way to learn programming is to see code in action:

<iframe style="width: 100%; height: 600px" src="http://embed.plnkr.co/p9vMvlzEwUOOlcP2FsUG" frameborder="0" allowfullscren="allowfullscren"></iframe>

I have kept the following notes for future reference:

Angular CLI helps development to debugging, testing to deploying the Angular apps.

Here is the terminology:

`angular-cli` - refers to Angular 2 

`@angular/cli` - refers to Angular 4

To install  `npm install -g @angular/cli`

The underlying language used is `typescript` which is translated to javascript using `babel`.

The task manager (like `gulp`, `grunt`) used by Angular CLI is `webpack`.

Old apps were page centric, modern apps are component based.

4 pillars of Angular 4

	1. Component - encapsulates the template (html), data (variables) but not source of data and the behaviour (functions) of a view.
	2. Directives - bridges the gap between backend and front end. Used for DOM manipulation.
	3. Routers - takes care of navigation between components.
	4. Services - reusable tags primarily used for manipulating DOM elements

# Adding a component

create a `mycomp.component.ts` file 

<pre><code class="typecript">
import {Component} from '@angular/core'

@Component({
selector:'my-component',
template:'welcome to my custom component'
})

export class MyComponent{
    
}
</code></pre>

and add component reference to `app.module.ts` in `declarations` parameter of `@NgModule`

<pre><code class="typecript">
import { MyComponent } from './mycomp.component';

@NgModule({
  declarations: [
    AppComponent, MyComponent
  ],
  imports: [
    BrowserModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
</code></pre>

# Adding a template file to a component

Create a file `footer.component.html` and replace the `template` key in `@Component` of a component `templateUrl:'./footer.component.html'`.

# One way binding

Add properties to component class:

<pre><code class="typecript">
export class FooterComponent {

    title = "welcome to footer component"

    courses = ['Angular', 'React', 'jQuery']

}
</code></pre>

And bind them like this:

<pre><code class="typecript">
{{title}}

<ul>
    <li *ngFor="let course of courses">
        {{course}}
    </li>
</ul>
</code></pre>

# Adding a service

Add a file `course.service.ts`

<pre><code class="typecript">
import { Injectable } from '@angular/core'

@Injectable()

export class CourseService {

    getCourses() {
        return ['Angular', 'React', 'jQuery'];
    }
}
</code></pre>

Add the reference inside `app.module.ts`'s `@NgModule`

`providers: [CourseService]`

Inject it in a component through it's constructor:

<pre><code class="typecript">
    constructor(cs: CourseService) {
        this.courses = cs.getCourses();
    }
</code></pre>

# Create a component from CLI

Fire the command `ng g c newComponent`.

There are 5 types of binding are supported

1. Property binding `[]` - bind the ts component property with html template property
2. Event binding `()` - binding the html template event to ts component
3. Two way data binding `[()]` - for component to template and vice versa data flow
4. Class binding - e.g.: [class.active]. Is used to add/remove a CSS class
2. Style binding - used to set the CSS style rules

# Property binding

Add a property to class `profilePic = "http://lorempixel.com/400/200"`

Use the property in the component `<img [src]=profilePic />`

# Add Bootstrap to Angular app

As of this writing the most stable version of Bootstrap is 3.3. Hence, head over to http://getbootstrap.com/docs/3.3/getting-started/#download and et CDN link under Bootstrap CDN somewhat like this:

<pre><code class="typecript">
<!-- Latest compiled and minified CSS -->
<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css" integrity="sha384-BVYiiSIFeK1dGmJRAkycuHAHRg32OmUcww7on3RYdg4Va+PmSTsz/K68vbdEjh4u" crossorigin="anonymous">
</code></pre>

Add this to `index.html`

# Use event binding

Add a button like this:

`<button class="btn btn-danger" (click)="clickHandler($event)">click me</button>`

And it's corresponding event handler in the component:

<pre><code class="typecript">
    clickHandler($event) {
        console.log($event);
    }
</code></pre>

# Using 2 way data binging

`<input type="text" [(ngModel)]="currentCity" /> {{currentCity}}`

This is similar to

`<input type="text" [value]="currentCity" (input)="currentCity=$event.target.value" />`

# Class binding

With a property isActive in the component, this

`<button class="btn btn-danger" [class.active]="isActive" >automatic active - click me</button>`

is equal to

`<button class="btn btn-danger active" >manually active - click me</button>`

# Style binding

We can set the style properties of an element using style properties

`<button class="btn btn-danger" [style.backgroundColor]="isActive?'green':'red'" >click me</button>`

# Inputs

Set a input property in the child component

<pre><code class="typecript">
@Component({
    selector: 'header-component',
    template: 'welcome to header component {{dataFromParentComponent}}',
    inputs: ['dataFromParentComponent']
})

export class HeaderComponent {
    
    dataFromParentComponent = ""; //or @Input dataFromParentComponent = "";

}
</code></pre>

Notice that there is no value assigned to `dataFromParentComponent`.

In the parent component, set the value of this input with it's own property:

<pre><code class="typecript">
@Component({
    selector: 'my-component',
    template: `<header-component [dataFromParentComponent]="myComponentData" ></header-component>`
})

export class MyComponent {

    myComponentData = "Parent data"

}
</code></pre>
