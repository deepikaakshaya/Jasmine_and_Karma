# Jasmine + Karma
## Introduction
*  __Jasmine__ is an open-source behavior-driven __testing framework__ and __karma__ is a __JavaScript Test Runner__
- There are 3 types of tests
	-   Unit tests
	-   Integration tests
	-   End-to-End (e2e) tests
- A unit test is the process of examining the specific part of the application and make sure it is working correctly and most importantly unit tests are written by developers
- Unit testing in Angular refers to the process of testing individual units of code

 ## What is Jasmine in Angular?
 - It help us to check for bugs in your code easily
 - It provides utilities that can be used to run automated tests for both synchronous and asynchronous code
 - **Jasmine** is also dependency free and doesn't require a DOM

## What is Karma in Angular?
- Karma is a JavaScript test runner that __runs __  the __unit test snippet(piece)__ in Angular.
- Karma also ensures the __result__ of the test is printed out either in the __console or in the file log__.
- By default, Angular runs on Karma. Other test runners include Mocha and Jasmine.
- Karma provides tools that make it easier to call Jasmine tests while writing code in Angular

##  Environment config
*  you must have Node js and npm configured on your system. Skip this step, If you have already configured otherwise follow this __set up Node and NPM__ on your device.
*  [Downloading and installing Node.js and npm](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm)
- Also, you must have installed the latest version of Angular CLI on your system.

```
npm install -g @angular/cli@latest
```

- If Node, NPM, and Angular CLI configured adequately, then go to the next step

## Setting Up Angular App
- Next, install the Angular project by running the below command:
- eg: unit-test is the name for projectname
```
ng new projectname 
```

- Head over to the project folder by using the following command:
```
cd unit-test
```

- Start the app on the browser:
```
ng serve 
```

- Now, you can view your app on the browser on the following port: [localhost:4200](http://localhost:4200/).

## Testing Example
- An Angular component is a collection of HTML template and a TypeScript class. So, to test a component first, we need to create a component

```
ng generate component user
```

- user.component.ts 

```
import { Component, OnInit } from '@angular/core';
import { UserService } from './user.service';
  
@Component({
 selector: 'app-user',
 templateUrl: './user.component.html',
 styleUrls: ['./user.component.css'],
 providers: [UserService]
})

export class UserComponent implements OnInit {
 isLoggedIn :Boolean= false;
 user!: { name: string; };

 constructor(private userService: UserService){ }

	ngOnInit()
	{
		this.user = this.userService.user;
	}
}
```

* user.component.html

```
<div *ngIf="isLoggedIn" >
 		<h1> User logged in</h1>
 		<p>User is {{ user.name }}</p>
	</div>

<div *ngIf="!isLoggedIn" >
 	<h1> User not logged in</h1>
 	<p>Please login in first</p>

</div>
```
* user.service.ts
```
export class UserService {
	 user ={ 
		 name :'Dennis Ritchie'
	 };
}
```
*   user.component.spec.ts

``` 
import { ComponentFixture, TestBed } from '@angular/core/testing';
import { UserComponent } from './user.component';
import { UserService } from './user.service';

describe('UserComponent', () => {

 let component: UserComponent;
 let fixture: ComponentFixture<UserComponent>;

 beforeEach(async () => {
 	await TestBed.configureTestingModule({
 	declarations: [ UserComponent ]
 }).compileComponents();

 });

 beforeEach(() => {
 	fixture = TestBed.createComponent(UserComponent);
 	component = fixture.componentInstance;
 	fixture.detectChanges();
 });

 
 it('should create an instance', () => {
 	expect(component).toBeTruthy();
 });

 it('It must use the user name from the service', () => {
	 let fixture =TestBed.createComponent(UserComponent);
	 let app =fixture.debugElement.componentInstance;
	 let userService = fixture.debugElement.injector.get(UserService);
	 fixture.detectChanges();
	 expect(userService.user.name).toEqual(app.user.name);
 });

 it('It must create the app', () => {
	 let fixture =TestBed.createComponent(UserComponent);
	 let app =fixture.debugElement.componentInstance;
	 expect(app).toBeTruthy();
 });
});
```

- You need to use the **ng test** command to start testing an Angular component

```
ng test
```

- Above command built the app in watch mode and launched the karma
- The **ng test** command opened the watch mode in karma and startup the testing environment

## My Sample Code output
* I added some content in the user component
*  Now, as you can see in the screenshot of specs, this means we passed the test for user
* ![output](https://user-images.githubusercontent.com/55552785/125243815-34360400-e30c-11eb-9ce0-c295eab1bfa9.JPG)

* Here you can see all my old components also, just refer only the user component 
*  Status of my code in terminal below
 ✔ Browser application bundle generation complete.
Chrome 91.0.4472.114 (Windows 10): Executed 6 of 6 SUCCESS (0.221 secs / 0.176 secs)
TOTAL: 6 SUCCESS

## Explanation of Testing Example

- The Angular testing package includes two utilities called `TestBed` and `async`. 
- `TestBed` is the main Angular utility __package__.
- ![Angular Unit Testing Example Flow](https://blog.logrocket.com/wp-content/uploads/2018/10/angular-unit-testing-example-flow.jpeg)
- The `describe` container contains different blocks (`it`, `beforeEach`, `xit`, etc.). `beforeEach` runs before any other block. Other blocks do not depend on each other to run.
	- From the example of my file `user.component.spec.ts` file, the first block is the `beforeEach` inside the container (`describe`). This is the only block that runs before any other block (`it`). The declaration of the app module in `app.module.ts` file is simulated (declared) in the `beforeEach` block. The component (`UserComponent`) declared in the `beforeEach` block is the main component we want to have in this testing environment. The same logic applies to other test declaration.
- The `compileComponents` object is called to compile your component’s resources like the template, styles etc
-  You might not necessarily compile your component if you are using webpack
-  fixture ---> to hold our created component 
-  The`fixture.debugElement.componentInstance` creates an instance of the class (`UserComponent`) 
-  The fixture creates a wrapper around a component instance, The fixture **TestBed.createComponent()** method allows accessing the component and its template.
-  After creating the component, an instance of the created component (`detectChanges`) to simulate running on the browser environment is called

## Some Jasmine Methods:
-	**it()**: Declaration of a particular test
-   **describe()**: It’s a suite of tests
-   **expect()**: Expect some value in true form

## Mock HTTP 
* you can use some HttpTestingModule, etc..  for testing the app components and services
* It act like backend services as mock application
