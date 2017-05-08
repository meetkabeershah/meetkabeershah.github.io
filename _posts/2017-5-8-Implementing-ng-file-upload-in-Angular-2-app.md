---
layout: post
title: Implementing ng-file-upload in Angular 2 app
---

![Upload file](http://www.uploadify.com/wp-content/themes/uploadify/img/splash.png)

[courtesy](http://www.uploadify.com/)

We needed to implement drag drop file input feature in one of our [Angular 2][1] app.

We selected [ng-file-upload][2] for this.

We tried to follow the [help page][3]. As suggested, implemented [`drag-upload-input.html`][4] & [`drag-upload-input.component.ts`][5] like the following:

**drag-upload-input.html**

    <!-- we only need single file upload -->
    <input type="file" ng2FileSelect [uploader]="uploader" />

**drag-upload-input.component.ts**

    import { Component } from '@angular/core';
    import { FileUploader } from 'ng2-file-upload';
    
    // const URL = '/api/';
    const URL = 'https://evening-anchorage-3159.herokuapp.com/api/';
    
    @Component({
      moduleId: module.id,
      selector: 'drag-upload-input',
      templateUrl: './drag-upload-input.html'
    })
    export class DragUploadInput {
      public uploader: FileUploader = new FileUploader({ url: URL });
      public hasBaseDropZoneOver: boolean = false;
      public hasAnotherDropZoneOver: boolean = false;
    
      public fileOverBase(e: any): void {
        this.hasBaseDropZoneOver = e;
      }
    
      public fileOverAnother(e: any): void {
        this.hasAnotherDropZoneOver = e;
      }
    }

The [`app.module.ts`][6] has got `FileUploadModule` like this:

    // File upload modules
    import { FileUploadModule } from 'ng2-file-upload';
    import { DragUploadInput } from './file-upload/drag-upload-input.component';
    
    //other imports
    
    @NgModule({
      imports: [ ... other imports
    FileUploadModule
    ],
      declarations: [  ... other declarations
    DragUploadInput],
      bootstrap: [AppComponent]
    })
    export class AppModule { }

And the [`systemjs.config.js`][7] looks like this:

    (function (global) {
      System.config({
        // map tells the System loader where to look for things
        map: {
          // other libraries
          'ng2-file-upload': 'node_modules/ng2-file-upload',
        },
        packages: {
    	  // other packages
          ng2-file-upload': {
            main: 'ng2-file-upload.js',
            defaultExtension: 'js'
          }
        }
      });
    })(this);


  [1]: https://angular.io/
  [2]: https://github.com/valor-software/ng2-file-upload
  [3]: http://valor-software.com/ng2-file-upload/
  [4]: https://github.com/valor-software/ng2-file-upload/blob/development/demo/src/app/components/file-upload/simple-demo.html
  [5]: https://github.com/valor-software/ng2-file-upload/blob/development/demo/src/app/components/file-upload/simple-demo.ts
  [6]: https://github.com/valor-software/ng2-file-upload/blob/development/demo/src/app/app.module.ts
  [7]: http://stackoverflow.com/a/37167153/2404470
