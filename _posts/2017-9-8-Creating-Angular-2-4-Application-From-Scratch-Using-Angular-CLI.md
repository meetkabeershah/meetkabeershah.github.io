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

<code><pre>
import { Injectable } from '@angular/core';

@Injectable()
export class ServiceNameService {

  constructor() { }

}
</pre></code>

A service has to have a few public methods.

**Adding an input to the Angular 4 app**

Assuming that we have 2 components:

 - `parent-component`
 - `child-component`

We wanted to pass some value from `parent-component` to `child-component` i.e. an `@Input` from `parent-component.html` to `child-component.ts`. Below is an example which explains the implementation:

`parent-component.html` looks like this:

`<child-component [someInputValue]="'Some Input Value'"></child-component>`

`child-component.ts` looks like this:

<code><pre>
import { Component, OnInit, Input } from '@angular/core';

@Component({
  selector: 'child-component',
  templateUrl: './child-component.html'
})
export class ChildComponent implements OnInit {

  @Input() someInputValue: String;

  constructor() {
    console.log('someInputValue in constructor ************** ', this.someInputValue); //someInputValue in constructor ************** undefined
  }

  ngOnInit() {
    console.log('someInputValue  in ngOnInit ************** ', this.someInputValue); //someInputValue  in ngOnInit ************** Some Input Value
  }
}
</pre></code>

Notice that the value of the `@Input` value is available inside `ngOnInit()` and not inside `constructor()`.

`ngOnInit()`, `ngOnChanges()` and `ngOnDestroy()` etc. are lifecycle methods. `ngOnChanges()` will be the first to be called, before `ngOnInit()`, when the value of a bound property changes, it will NOT be called if there is no change. `ngOnDestroy()` is called when the component is removed. To use it, `OnDestroy` needs to be `implement`ed by the class.

