---
layout: post
title: Creating Angular 2/4 Application From Scratch Using Angular CLI
---

![Angular CLI](https://aymen.co/wp-content/uploads/2017/01/angular-cli.jpg)

[Courtesy](https://aymen.co/javascript/angular-cli/)

**Installing Angular Dependencies**
 - Install a stable version of [Node](https://nodejs.org/) (if not already installed) and verify the installation using `node -v`
 - Install [TypeScript](http://www.typescriptlang.org/) using [command `npm install -g typescript`](http://www.typescriptlang.org/index.html#download-links)
 - Download and install [Angular CLI](https://cli.angular.io/) using command `npm install -g @angular/cli`

`Angular` is a component oriented framework. Many components needs to be created to make the whole application. A component is a group of [custom elements, `HTML` elements, `ShadowDOM` & `HTML` imports.](//xameeramir.github.io/Custom-Elements-Shadow-DOM-Templates-in-HTML-by-Examples/)

**Creating the Angular 4 app using Angular CLI**

To create a fresh new Angular 4 app, use command `ng new newAppName`. This command takes some time to execute.

`package.json` - takes care of the development and app dependencies / packages / commands to execute

`src\main.ts` - takes care of the scaffolding the entire

`src\app\app.module.ts` - any newly created module has to added to the `declarations` and services has to be provided to the `providers` key parameter  of the function `@NgModule` to make them accessible across the entire application

**Run the Angular 4 app using Angular CLI**

To run the freshly created app using CLI, use command `ng serve` which will run the app on [http://localhost:4200/](http://localhost:4200/).

**Add a component to the Angular 4 app using Angular CLI**

To add a new Angular 4 component to the app, use command `ng g component componentName`. After execution of this command, Angular CLI adds a folder `component-name` under `src\app`. Also, the references of the same is added to `src\app\app.module.ts` file automatically.

A component shall have a `@Component` decorator function followed by a `class` which needs to be `export`ed. The `@Component` decorator function accepts meta data.

**Add a component to specific folder of the Angular 4 app using Angular CLI**

To add a new component to a specific folder use the command `ng g component folderName/componentName`

**Add a service to the Angular 4 app using Angular CLI**

An Angular 2 service is simply a javascript function along with it's associated properties and methods, that can be included (via dependency injection) into Angular 2 components.

To add a new Angular 4 service to the app, use the command `ng g service serviceName`. On creation of the service, the Angular CLI shows an error:

![WARNING Service is generated but not provided, it must be provided to be used](https://i.stack.imgur.com/ZZwBC.png)

To solve this, we need to provide the service reference to the `src\app\app.module.ts` inside `providers` input of `@NgModule` method.

Initially, the default code in the service is:

<pre><code>
import { Injectable } from '@angular/core';

@Injectable()
export class ServiceNameService {

  constructor() { }

}
</code></pre>

A service has to have a few public methods.

**Adding an input to the Angular 4 app**

Assuming that we have 2 components:

 - `parent-component`
 - `child-component`

We wanted to pass some value from `parent-component` to `child-component` i.e. an `@Input` from `parent-component.html` to `child-component.ts`. Below is an example which explains the implementation:

`parent-component.html` looks like this:

`<child-component [someInputValue]="someInputValue"></child-component>`

`parent-component.ts` looks like this:

<pre><code>  
  class ParentComponent {

  someInputValue = 'Some Input Value';

}
</code></pre>

`child-component.html` looks like this:

`<p>Some Input Value {{someInputValue}}</p>`

`child-component.ts` looks like this:

<pre><code>
import { Component, OnInit, Input } from '@angular/core';

@Component({
  selector: 'child-component',
  templateUrl: './child-component.html'
})
export class ChildComponent implements OnInit {

  @Input() someInputValue: String = "Some default value";

  @Input()
  set setSomeInputValue(val) {
    this.someInputValue += " modified";
  }

  constructor() {
    console.log('someInputValue in constructor ************** ', this.someInputValue); //someInputValue in constructor ************** undefined
  }

  ngOnInit() {
    console.log('someInputValue  in ngOnInit ************** ', this.someInputValue); //someInputValue  in ngOnInit ************** Some Input Value
  }
}
</code></pre>

Notice that the value of the `@Input` value is available inside `ngOnInit()` and not inside `constructor()`.

**Objects reference behaviour in Angular 2 / 4**

In Javascript, objects are stored as references:

<iframe width="100%" height="300" src="//jsfiddle.net/xameeramir/dftagmaf/embedded/js/" allowfullscreen="allowfullscreen" frameborder="0"></iframe>

This exact behaviour can be re-produced with the help of Angular 2 / 4. Below is an example which explains the implementation:

`parent-component.ts` looks like this:

<pre><code>  
  class ParentComponent {

  someInputValue = {input: 'Some Input Value'};

}
</code></pre>

`parent-component.html` looks like this:

<pre><code>  
{{someInputValue.input}}

<child-component [someInputValue]="someInputValue"></child-component>

</code></pre>

`child-component.html` looks like this:

<pre><code>

<p>Some Input Value {{someInputValue}}</p>
<button (click)="changeInput()">change input</button>

</code></pre>

`child-component.ts` looks like this:

<pre><code>
import { Component, OnInit, Input } from '@angular/core';

@Component({
  selector: 'child-component',
  templateUrl: './child-component.html'
})
export class ChildComponent implements OnInit {

  @Input() someInputValue = {input:"Some default value"};

  @Input()
  set setSomeInputValue(val) {
    this.someInputValue.input += " set from setter";
  }

  constructor() {
    console.log('someInputValue in constructor ************** ', this.someInputValue); //someInputValue in constructor ************** undefined
  }

  ngOnInit() {
    console.log('someInputValue  in ngOnInit ************** ', this.someInputValue); //someInputValue  in ngOnInit ************** Some Input Value
  }

  changeInput(){
    this.someInputValue.input += " changed";
  }
}
</code></pre>

The function `changeInput()` will change the value of `someInputValue` inside both `ChildComponent` &amp; `ParentComponent` because of their reference. Since, `someInputValue` is referenced from `ParentComponent`'s `someInputValue` **object** - the change in `ChildComponent`'s `someInputValue` **object** changes the value of `ParentComponent`'s `someInputValue` **object**. *THIS IS NOT CORRECT*. The references shall never be changed.

**Angular 4 life cycle methods**

`ngOnInit()`, `ngOnChanges()` and `ngOnDestroy()` etc. are lifecycle methods. `ngOnChanges()` will be the first to be called, before `ngOnInit()`, when the value of a bound property changes, it will NOT be called if there is no change. `ngOnDestroy()` is called when the component is removed. To use it, `OnDestroy` needs to be `implement`ed by the class.

**DOM Manipulation in Angular 4 app**

To manipulate the DOM in Angular 2/4 apps, we need to `implement` the method `ngAfterViewInit()` of `AfterViewInit`. The method `ngAfterViewInit()` is called when the bindings of the children directives have been checked for the first time. In other words, **when** the view is initially rendered.

The `@ViewChild` provides access to `nativeElement`. It is recommended to not access `nativeElement` inside the `ngAfterViewInit()` because it is not browser safe. Also, it's not supported by web workers. Web workers will never know when the DOM updates. 

The right way is to use `renderer`. The renderer needs to be injected to the component constructor. We need to provide an `id` reference to the `HTML` element on the view something like this:

`<p #p1></p>`

It shall be accessed by the corresponding coponent `.ts` file, something like this:

<pre><code>
export class SampleComponent implements AfterViewInit {

  @ViewChild("p1") p1;

  constructor(private renderer: Renderer2) //Renderer set to be depreciated soon
  { }

  ngAfterViewInit() {

    //recommended DOM manipulation approach
    this.renderer.setStyle(this.p1.nativeElement, //setElementStyle for soon to be depreciate Renderer
      'color',
      'red');

    //not recommended DOM manipulation approach
    //this.p1.nativeElement.style = "color:blue;";
  }

}
</code></pre>

**Programmatically add components to DOM in Angular 2/4 app**

We need to use `ngAfterContentInit()` lifecycle method from `AfterContentInit`. It is called after the directive content has been fully initialized.

In the `parent-component.html`, add the a `div` like this:

`<div #container> </div>`

The `parent-component.ts` file looks like this:

<pre><code>

class ParentComponent implements AfterContentInit {

  @ViewChild("container", { read: ViewContainerRef }) divContainer

  constructor(private componentFactoryResolver: ComponentFactoryResolver) { }

  ngAfterContentInit() {
    let childComponentFactory = this.componentFactoryResolver.resolveComponentFactory(childComponent);
    this.divContainer.createComponent(childComponentFactory);
    let childComponentRef = this.divContainer.createComponent(childComponentFactory);
    childComponentRef.instance.someInputValue = "Assigned value";

  }
}
</code></pre>

Inside `src\app\app.module.ts`, add the following entry to the `@NgModule()` method parameters:

<pre><code>
  entryComponents:[
    childComponent
  ],
</code></pre>


Notice that we're not accessing the `div#container` using the `@ViewChild("container") divContainer` approach. We need it's reference instead of the `nativeElement`. We will access it as `ViewContainerRef`:

`@ViewChild("container", {read: ViewContainerRef}) divContainer`

The `ViewContainerRef` has a method called `createComponent()` which requires a component factory to be passed as a parameter. For the same, we need to inject a `ComponentFactoryResolver`. It has a method which basically loads a component.

