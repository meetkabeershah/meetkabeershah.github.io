---
layout: post
title: Creating Angular 2/4 Application From Scratch Using Angular CLI
---

![Angular CLI](https://aymen.co/wp-content/uploads/2017/01/angular-cli.jpg)

[Courtesy](https://aymen.co/javascript/angular-cli/)

# Creating an Angular 2/4 Application from Scratch using Angular CLI

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
