# TypeScript Style Guide

This is the TypeScript style guide that we use internally at Contorion! It is *semi-reasonable*, but it's more important that we keep a consistent look/feel of our code.


## Table of Contents

  0. [Introduction](#introduction)
  0. [Browser Compatibility](#browser-compatibility)
  0. [Files](#files)
  0. [Indentation](#indentation)
  0. [Max Line Length](#max-line-length)
  0. [Quotes](#quotes)
  0. [Comments](#comments)
    0. [Class](#class)
    0. [Inline](#inline)
    0. [Todo and XXX](#todo-and-xxx)
  0. [Variable Declarations](#variable-declarations)
  0. [Function Declarations](#function-declarations)
    0. [Anonymous Functions](#anonymous-functions)
  0. [Names](#names)
    0. [Variables, Modules, and Functions](#variables-modules-and-functions)
    0. [Use of var, let, and const](#use-of-var-let-and-const)
    0. [Types](#types)
    0. [Classes](#classes)
    0. [Class extends Native Class](#class-extends-native-class)
    0. [Interfaces](#interfaces)
    0. [Constants](#constants)
  0. [Statements](#statements)
    0. [Simple](#simple)
    0. [Compound](#compound)
    0. [Return](#return)
    0. [If](#if)
    0. [For](#for)
    0. [For..in](#for-in)
    0. [For..of](#for-of)
    0. [While](#while)
    0. [Do While](#do-while)
    0. [Switch](#switch)
    0. [Try](#try)
    0. [Continue](#continue)
    0. [Throw](#throw)
  0. [Whitespace](#whitespace)
  0. [Object and Array Literals](#object-and-array-literals)
  0. [Assignment Expressions](#assignment-expressions)
  0. [Typings](#assignment-expressions)
    0. [External](#external)
    0. [Internal](#internal)
  0. [=== and !== Operators](#===-and-!==-Operators)
  0. [Import](#import)
  0. [Conditional Import](#conditional-import)
  0. [Eval](#eval)
  0. [TSLint](#tslint)
    0. [Trailing Comma](#trailing-comma)
  0. [License](#license)

## Introduction
When developing software as an organization, the value of the software produced is directly affected by the quality of the codebase. 
Consider a project that is developed over many years and handled/seen by many different people.

If the project uses a consistent coding convention it is easier for new developers to read, preventing a lot of time/frustration spent figuring out the structure and characteristics of the code. 

For that purpose, we need to make sure we adhere to the same coding conventions across all of our products. This will not only help new developers, but it will also aid in quickly identifying potential flaws in the code, thereby reducing the brittleness of the code.

**[top](#table-of-contents)**

## Browser Compatibility
#### Desktop
  - Target evergreen browsers `ie >= 11`
  - Target modern browsers `ie >= 10`
  - IE 10 Should just work..
  - Avoid targeting older browsers `ie < 10` if at all possible
  - Edge >= 14
  - Firefox > 52 (46/48 -> acceptance tests)
  - Chrome > 58 
  - Safari >= 10.1

#### Tablet & Mobile
  ##### iOS (>=10)
  
  - Safari >= 10.3
  - Chrome (See Safari up to iOS 10)
  - Firefox (See Safari up to iOS 10)
  - Recheck with iOS 11!
  
  ##### Android (>= 4.5)
  
  - Android Browser >= 56 (Default Chrome)
  - Chrome (Same as desktop)
  - Firefox (Same as desktop)


**[top](#table-of-contents)**

## Files
  - All TypeScript files must have a ".ts" extension.
  - They should be all lower case, and only include letters, numbers, and periods.
  - Separation of architectural description is done with periods (e.g. `search.component.ts`).
  - Separation of words is done with hyphens (e.g. `search-input.component.ts`)
  - **All files should end in a new line.** This is necessary for some Unix systems.

**[top](#table-of-contents)**

## Indentation
  - The unit of indentation is four spaces.
  - **Never use tabs**, as this can lead to trouble when opening files in different IDEs/Text editors. 
  Most text editors have a configuration option to change tabs to spaces.

**[top](#table-of-contents)**

### Max Line Length

  - Lines must not be longer than 100 characters.
  - When a statement runs over 100 characters on a line, it should be broken up, ideally after a comma or operator.
  - When defining parameters, use separate lines when exceeding `max-line-length` of 100

  ```typescript
  class Person {
      protected fullName: string;

      constructor(
          public firstName: string,
          public lastName: string,
      ) {
          this.fullName = firstName + ' ' + lastName;
      }

      toString() {
          return this.fullName;
      }

      protected walkFor(millis: number) {
          console.log(this.fullName + ' is now walking.');

          // Wait for millis milliseconds to stop walking
          setTimeout(() => {
              console.log(this.fullName + ' has stopped walking.');
          }, millis);
      }
  }
  ```

**[top](#table-of-contents)**

## Quotes
  - Use single-quotes `''` for all strings, and use double-quotes `""` for strings within strings.
  - For multiple lines we use `` (backticks) 

  ```typescript
  // bad
  let greeting: string = "Hello World!";

  // good
  let greeting: string = 'Hello World!';

  // bad
  let html: string = "<div class='bold'>Hello World</div>";

  // bad
  let html: string = '<div class=\'bold\'>Hello World</div>';

  // good
  let html: string = '<div class="bold">Hello World</div>';
  
  // bad
  let multiLine: string = 'this \
                          is a multiline \
                          string';
  
  // good
  let multiLine: string = `this
                           is a multiline
                           string`;
  ```

**[top](#table-of-contents)**

## Comments
  - Comments are discouraged. The intent of strict typing is to be more descriptive and to make the use of comments obsolete.
  - Comments need to be clear, just like the code they are annotating.
  - Make sure your comments are meaningful.

The following example is a case where a comment is completely useless, and can actually make the code harder to read.

  ```typescript
  // Set index to zero.
  let index: number = 0;
  ```

### Class

  - As Typescript is already very descriptive and has types everywhere, nothing like [JSDoc](http://usejsdoc.org/) is used!
  - Be descriptive in naming variables, classes, methods so there is no need of (block) comments.

  ```typescript
  class Person {
      static GetPerson(name: string): Person {
          return new Person(name);
      }

      constructor(public name: string) { }

      walkFor(milliseconds: number): void {
          console.log(this.name + ' is now walking.');

          setTimeout(() => {
              console.log(this.name + ' has stopped walking.');
          }, milliseconds);
      }
  }
  ```

**[top](#table-of-contents)**

### Inline

  - Inline comments are comments inside of complex statements (loops, functions, etc).
  - Descriptive namings should be encouraged at all times.
  - Only when very strange cases occur & you feel some outsider might need help in understanding what you wrote.
  - Use `//` for all inline comments.
  - Keep comments clear and concise.
  - Place inline comments on a newline above the line they are annotating
  - Put an empty line before the comment.

  ```typescript
  // bad
  let lines: Array<string>; // Holds all the lines in the file.

  // good
  // Holds all the lines in the file.
  let lines: Array<string>;

  // bad
  function walkFor(name: string, millis: number): void {
      console.log(name + ' is now walking.');
      // Wait for millis milliseconds to stop walking
      setTimeout(() => {
          console.log(name + ' has stopped walking.');
      }, millis);
  }

  // good
  function walkFor(name: string, millis: number): void {
      console.log(name + ' is now walking.');

      // Wait for millis milliseconds to stop walking
      setTimeout(() => {
          console.log(name + ' has stopped walking.');
      }, millis);
  }
  ```

**[top](#table-of-contents)**

### Todo and XXX

`TODO` and `XXX` annotations help you quickly find things that need to be fixed/implemented.

  - Use `// TODO` to annotate solutions that need to be implemented.
  - It is recommended to use `// TODO` in combination with a (Git/Syntax) name.
  - Use `// XXX` to annotate problems that need to be fixed.
  - It is best to write code that doesn't need `TODO` and `XXX` annotations, but sometimes it is unavoidable.

**[top](#table-of-contents)**

## Variable Declarations

  - All variables must be declared prior to using them. This aids in code readability and helps prevent undeclared variables from being hoisted onto the global scope.

  ```typescript
  // bad
  console.log(a + b);

  let a: number = 2,
      b: number = 4;

  // good
  let a: number = 2;
  let b: number = 4;

  console.log(a + b);
  ```

  - Implied global variables should never be used.
  - You should never define a variable on the global scope from within a smaller scope.

  ```typescript
  // bad
  function add(a: number, b: number): number {
      // c is on the global scope!
      c = 6;

      return a + b + c;
  }
  
  // bad
  function add(a: number, b: number): number {
      // c is on the global scope!
      let c: number = 6;
  
      return a + b + c;
    }
  ```

  - Use one `let` keyword to define a block of variables.
  - Use one `let` keyword per declaration of a variable.
  - Place each declaration of a variable on a newline.

  ```typescript
  // bad
  let a: number = 2,
      b: number = 2,
      c: number = 4;
  
  // good
  let a: number = 2;
  let b: number = 2;
  let c: number = 4;
  
  // bad
  // b will be defined on global scope.
  let a = b = 2, c = 4;
  
  // bad
  let a: number, b: Array<string>, c: object;
    
  // good
  let a: number;
  let b: Array<string>;
  let c: object;
  ```

## Function Declarations

  - All functions must be declared before they are used.
  - Any closure functions should be defined right after the `let` declarations.

  ```typescript
  // bad
  function createGreeting(name: string): string {
      let message = 'Hello ';

      return greet;

      function greet() {
          return message + name + '!';
      }
  }

  // good
  function createGreeting(name: string): string {
      let message = 'Hello ';

      function greet() {
          return message + name + '!';
      }

      return greet;
  }
  ```

  - There should be no space between the name of the function and the left parenthesis `(` of its parameter list.
  - There should be one space between the right parenthesis `)` and the left curly `{` brace that begins the statement body.

  ```typescript
  // bad
  function foo (){
      // ...
  }
  
  // good
  function foo() {
      // ...
  }
  ```

  - The body of the function should be indented with 4 spaces.
  - The right curly brace `}` should be on a new line.
  - The right curly brace `}` should be aligned with the line containing the left curly brace `{` that begins the function statement.

  ```typescript
  // bad
  function foo(): string {
    return 'foo';}
  
  // good
  function foo(): string {
      return 'foo';
  }
  ```

  - For each function parameter
    - There should be no space between the parameter and the colon `:` indicating the type declaration.
    - There should be a space between the colon `:` and the type declaration.

  ```typescript
  // bad
  function greet(name:string) :string {
    // ...
  }
  
  // good
  function greet(name: string): string {
    // ...
  }
  ```

  - Always add a function return type even when there i.

  ```typescript
    // bad
    function greet(name:string) {
      // ...
    }

    // good
    function greet(name: string): void {
      // ...
    }
  ```


**[top](#table-of-contents)**

### Anonymous Functions

  - All anonymous functions should be defined as fat-arrow/lambda `() => { }` functions unless it is absolutely necessary to preserve the context in the function body.
  - All fat-arrow/lambda functions should have parenthesis `()` around the function parameters.
  - Even if there is only 1 parameter, always use parenthesis.
  - There should be a space between the right parenthesis `)` and the `=>`
  - There should be a space between the `=>` and the left curly brace `{` that begins the statement body.
  - The statement body should be indented 4 spaces.
  - The right curly brace `}` should be on a new line.
  - The right curly brace `}` should be aligned with the line containing the  left curly brace `{` that begins the function statement.
  
  ```typescript
  // bad
  element.addEventListener('click', (ev: Event)=>{alert('foo');});
  
  // good
  element.addEventListener('click', (ev: Event) => {
      alert('foo');
  });
  ```
  
  The interesting thing to note is that the `this` value (internally) is not actually bound to the arrow function. 
  Normal functions in JavaScript bind their own `this` value, however the `this` value used in arrow functions is actually fetched lexically from the scope it sits inside. 
  It has no `this`, so when you use `this` you’re talking to the outer scope.

  ```typescript
  // bad
  clickAlert() {
      let element = document.querySelector('div');

      this.foo = 'foo';

      element.addEventListener('click', function(ev: Event) {
          // this.foo does not exist!
          alert(this.foo);
      });
  }

  // good
  clickAlert() {
      let element = document.querySelector('div');

      this.foo = 'foo';

      element.addEventListener('click', (ev: Event) => {
          // TypeScript allows this.foo to exist!
          alert(this.foo);
      });
  }
  ```

**[top](#table-of-contents)**

## Names

  - All variable, function, class names should be formed with alphabetic characters `A-Z, a-z`.
  - We use UPPER_SNAKE_CASE for the global constants.

### Variables, Modules, and Functions

  - Variable, module, and function names should use lowerCamelCase.

### Use of var, let, and const

  - Use `const` where appropriate, for values that should never change.
  - Use `let` everywhere else.
  - Never use `var`!

**[top](#table-of-contents)**

### Types

  - Always favor type inference over explicit type declaration except for function return types
  - Always define the return type of functions.
  - Types should be used (no implicit `any`).
  - Arrays should be defined as `Array<type>` instead of `type[]`.
  - Some types don't have a 'shorter' syntax, so we go for consistency.
  - Never use the `any` type, it is always better to define an interface.

  ```typescript
  // bad
  let numbers = [];
    
  // bad
  let numbers: number[] = [];
  
  // good
  let numbers: Array<number> = [];
  ```

**[top](#table-of-contents)**

### Classes

  - Classes/Constructors should use UpperCamelCase (PascalCase).
  - Opening `{` should be on the same line as the class declaration.
  - Closing `}` should be vertically aligned with the declaration of the class.
  - `Private` and `private static` members in classes should be denoted with the `private` keyword.
  - `Protected` members in classes do not use the `private` keyword.
  - Default to using `protected` for all instance members.
  - Use `private` instance members sparingly.
  - Use `public` instance members only when they are used by other parts of the application.
  - Order of preference is followed like Robert C. Martin (Uncle Bob) advises coders to always put member variables at the top of the class (constants first, then private members) and methods should be ordered in such a way so that they read like a story that doesn't cause the reader to need to jump around the code too much. This is a more sensible way to organize code rather than by access modifier.
  - All public methods are right after the constructor. (As stated by TSLint recommendation rules)

  ```typescript
  class Person {
      protected fullName: string;

      constructor(public firstName: string, public lastName: string) {
          this.fullName = firstName + ' ' + lastName;
      }

      toString() {
          return this.fullName;
      }

      protected walkFor(millis: number) {
          console.log(this.fullName + ' is now walking.');

          // Wait for millis milliseconds to stop walking
          setTimeout(() => {
              console.log(this.fullName + ' has stopped walking.');
          }, millis);
      }
  }
  ```

**[top](#table-of-contents)**

### Class extends Native class

  - When a `Class` extends from a Native class, there is no import as this is native functionality.
  - To clarify what native classes are available, you can find all of them here: [Lib ES6 TS](https://github.com/Microsoft/TypeScript/blob/master/lib/lib.es6.d.ts)
  - These are available and automatically recognised by all proper IDE's by default. (_e.g. [WebStorm](https://www.jetbrains.com/webstorm/), [MS Visual Studio](https://www.visualstudio.com/)_)

  ```typescript
  class Person extends Touch {
      static GetPerson(name: string): Person {
          return new Person(name);
      }

      constructor(public name: string) { }

      walkFor(millis: number): void {
          console.log(this.name + ' is now walking.');

          setTimeout(() => {
              console.log(this.name + ' has stopped walking.');
          }, millis);
      }
  }
  ```

**[top](#table-of-contents)**

### Interfaces

  - Interfaces should use UpperCamelCase.
  - Interfaces should be prefaced with the capital letter I.
  - Only `public` members should be in an interface, leave out `protected` and `private` members.

  ```typescript
  interface IPerson {
      firstName: string;
      lastName: string;
      toString(): string;
  }
  ```

**[top](#table-of-contents)**

### Constants

  - All global constants should use UPPER_SNAKE_CASE.
  - All local constants should use regular variable naming.
  - All constants should be defined with the `const` keyword.

**[top](#table-of-contents)**

## Statements

### Simple

  - Each line should contain at most one statement.
  - A semicolon should be placed at the end of every simple statement.

  ```typescript
  // bad
  let greeting = 'Hello World'

  alert(greeting)

  // good
  let greeting = 'Hello World';

  alert(greeting);
  ```

**[top](#table-of-contents)**

### Compound

Compound statements are statements containing lists of statements enclosed in curly braces `{}`.

  - The enclosed statements should start on a newline.
  - The enclosed statements should be indented 4 spaces.

  ```typescript
  // bad
  if (condition === true) { alert('Passed!'); }

  // good
  if (condition === true) {
      alert('Passed!');
  }
  ```
  - The left curly brace `{` should be at the end of the line that begins the compound statement.
  - The right curly brace `}` should begin a line and be indented to align with the line containing the left curly brace `{`.

  ```typescript
  // bad
  if (condition === true)
  {
      alert('Passed!');
  }

  // good
  if (condition === true) {
      alert('Passed!');
  }
  ```

  - **Braces `{}` must be used around all compound statements** even if they are only single-line statements.

  ```typescript
  // bad
  if (condition === true) alert('Passed!');

  // bad
  if (condition === true)
      alert('Passed!');

  // good
  if (condition === true) {
      alert('Passed!');
  }
  ```

If you do not add braces `{}` around compound statements, it makes it very easy to accidentally introduce bugs.

  ```typescript
  if (condition === true)
      alert('Passed!');
      return condition;
  ```

It appears the intention of the above code is to return if `condition === true`, but without braces `{}` the return statement will be executed regardless of the condition.

  - Compount statements do not need to end in a semicolon `;` with the exception of a `do { } while();` statement.

**[top](#table-of-contents)**

### Return

  - If a `return` statement has a value you should not use parenthesis `()` around the value.
  - The return value expression must start on the same line as the `return` keyword.

  ```typescript
  // bad
  return
      'Hello World!';

  // bad
  return ('Hello World!');

  // good
  return 'Hello World!';
  ```

  - It is recommended to take a return early approach whenever possible.


  ```typescript
  // bad
  function getHighestNumber(a: number, b: number): number {
      let out = b;

      if (a >= b) {
          out = a;
      }
  
      return out;
  }

  // good
  function getHighestNumber(a: number, b: number): number {
      if (a >= b) {
          return a;
      }
  
      return b;
  }
  ```

  - Always **explicitly define a return type**. This can help TypeScript validate that you are always returning something that matches the correct type.
  - When there is nothing to return use `: void`.

  ```typescript
  // bad
  function getPerson(name: string) {
      return new Person(name);
  }

  // good
  function getPerson(name: string): Person {
      return new Person(name);
  }

  // bad
  function greet(name:string) {
    // ...
  }

  // good
  function greet(name: string): void {
    // ...
  }
  ```

**[top](#table-of-contents)**

### If

  - Alway be explicit in your `if` statement conditions.

  ```typescript
  // bad
  function isString(str: any) {
      return !!str;
  }

  // good
  function isString(str: any) {
      return typeof str === 'string';
  }
  ```

Sometimes simply checking falsy/truthy values is fine, but the general approach is to be explicit with what you are looking for. This can prevent a lot of unnecessary bugs.

If statements should take the following form:

  ```typescript
  if (/* condition */) {
      // ...
  }
  
  if (/* condition */) {
      // ...
  } else {
      // ...
  }
  ```

  - When you need an `else if` then you should always use a switch statement instead.
  - If the switch is not easy because of the conditional, then you should find a way to make this work.

  ```typescript
  // bad
  if (/* condition */) {
      // ...
  } else if (/* condition */) {
      // ...
  } else {
      // ...
  }

  // good
  switch (/* expression */) {
      case /* expression */:
          // ...
          /* termination */
      default:
          // ...
  }
  ```

**[top](#table-of-contents)**

### For

For statements are discouraged should have the following form:

  ```typescript
  for (/* initialization */; /* condition */; /* update */) {
      // ...
  }

  let keys = Object.keys(/* object */),
      length = keys.length;

  for (let i = 0; i < length; i++) {
      // ...
  }
  ```

Object.prototype.keys is supported in `ie >= 9`.

  - Use Object.prototype.keys in lieu of a `for...in` statement.

**[top](#table-of-contents)**

### For in

For..in statemenst are strongly encouraged have the following form:

  ```typescript
  let list = [4, 5, 6];

  for (let i in list) {
      console.log(entry);
      // "0", "1", "2"
  }
  ```

**[top](#table-of-contents)**

### For of

For..of statements are strongly encouraged and have the following form:

  ```typescript
  let list = [4, 5, 6];

  for (let i of list) {
      console.log(entry);
      // "4", "5", "6"
  }
  ```

**[top](#table-of-contents)**

### While

While statements should have the following form:

  ```typescript
  while (/* condition */) {
      // ...
  }
  ```

**[top](#table-of-contents)**

### Do While

  - Do while statements should be avoided unless absolutely necessary to maintain consistency.
  - Do while statements must end with a semicolon `;`

Do while statements should have to following form:

  ```typescript
  do {
      // ...
  } while (/* condition */);
  ```

**[top](#table-of-contents)**

### Switch

Switch statements should have the following form:

  ```typescript
  switch (/* expression */) {
      case /* expression */:
          // ...
          /* termination */
      default:
          // ...
  }
  ```

  - Each switch group except default should end with `break`, `return`, or `throw`.
  - Each switch group should have a default.

**[top](#table-of-contents)**

### Try

  - Try statements should be avoided whenever possible. They are not a good way of providing flow control.

Try statements should have the following form:

  ```typescript
  try {
      // ...
  } catch (error: Error) {
      // ...
  }

  try {
      // ...
  } catch (error: Error) {
      // ...
  } finally {
      // ...
  }
  ```

**[top](#table-of-contents)**

### Continue

  - It is recommended to take a continue-first approach in all loops.

**[top](#table-of-contents)**

### Throw

  - Avoid the use of the throw statement unless absolutely necessary.
  - Flow control through try/catch exception handling is not recommended.

**[top](#table-of-contents)**

## Whitespace

Blank lines improve code readability by allowing the developer to logically group code blocks. Blank spaces should be used in the following circumstances.

  - A keyword followed by left parenthesis `(` should be separated by 1 space.

  ```typescript
  // bad
  if(condition) {
      // ...
  }

  // good
  if (condition) {
      // ...
  }
  ```

  - All operators except for period `.`, left parenthesis `(`, and left bracket `[` should be separated from their operands by a space.

  ```typescript
  // bad
  let sum = a+b;

  // good
  let sum = a + b;

  // bad
  let name = person . name;

  // good
  let name = person.name;

  // bad
  let item = items [4];

  // good
  let item = items[4];
  ```

  - No space should separate a unary/incremental operator `!x, -x, +x, ~x, ++x, --x` and its operand.

  ```typescript
  // bad
  let neg = - a;

  // good
  let neg = -a;
  ```

  - Each semicolon `;` in the control part of a `for` statement should be followed with a space.

  ```typescript
  // bad
  for (let i = 0;i < 10;i++) {
      // ...
  }

  // good
  for (let i = 0; i < 10; i++) {
      // ...
  }
  ```

**[top](#table-of-contents)**

## Object and Array Literals

  - Use curly braces `{}` instead of `new Object()`.
  - Use brackets `[]` instead of `new Array()`.

**[top](#table-of-contents)**

## Assignment Expressions

  - Assignment expressions inside of the condition block of `if`, `while`, and `do while` statements should be avoided.

  ```typescript
  // bad
  while (node = node.next) {
      // ...
  }

  // good
  while (typeof node === 'object') {
      node = node.next;

      // ...
  }
  ```

**[top](#table-of-contents)**

## === and !== Operators

  - It is better to use `===` and `!==` operators whenever possible.
  - `==` and `!=` operators do type coercion, which can lead to headaches when debugging code.

**[top](#table-of-contents)**


## Import
  
  - When making an import, watch out for the max line length
  - To assure more readability, we list the imports on new lines when there are >= 3
  
  ```typescript
  // bad
  import { ITouchExtended, NavigationService, navigationService } from '../services/navigation.service';
  
  // good
  import { 
    ITouchExtended,
    NavigationService,
    navigationService,
  } from '../services/navigation.service';
  ```
  
**[top](#table-of-contents)**

  
## Conditional Import

  - When conditionally importing the first module instantiation we need to add the `webpackChunkname`.
  - We add a `webpackChunkname` to easily debug and retrieve the used module.
  - This might also have cause the crashing of Webkit. 
  
  ```typescript
  // bad
  if (navigationElements.length) {
    import ('./components/navigation.component')
        .then(({ NavigationComponent }) => {
            navigationElements.forEach((navigationElement) => {
                <Component> NavigationComponent.loadByElement(navigationElement);
            });
        });
  }
  
  // good
  if (navigationElements.length) {
      import (/* webpackChunkName: "navigation" */ './components/navigation.component')
          .then(({ NavigationComponent }) => {
              navigationElements.forEach((navigationElement) => {
                  <Component> NavigationComponent.loadByElement(navigationElement);
              });
          });
  }
  ```

**[top](#table-of-contents)**  

## Typings

### External

  - Typings are sometimes packaged with node modules, in this case you don't need to do anything
  - Use [typings](https://github.com/typings/typings) for all external library declarations not included in `node_modules`
  - Actively add/update/contribute typings when they are missing

### Internal

  - Create declaration files `.d.ts` for your interfaces instead of putting them in your `.ts` files
  - Let the TypeScript compiler infer as much as possible
  - Never avoid defining types when it is unnecessary

  ```typescript
  // bad
  let a = 2;
  
  // good
  let a: number = 2;
  ```

  - Always define the return type of functions, this helps to make sure that functions always return the correct type
  - When the function is not returning anything, then you should use `: void`

  ```typescript
  // bad
  function sum(a: number, b: number) {
      return a + b;
  }

  // good
  function sum(a: number, b: number): number {
      return a + b;
  }
  ```

**[top](#table-of-contents)**

## Eval

  - **Never use eval**
  - **Never use the Function constructor**
  - **Never pass strings to `setTimeout` or `setInterval`**

**[top](#table-of-contents)**

## TSLint

  Linting your code is very helpful for preventing minor issues that can escape the eye during development. We use TSLint (written by Palantir) for our linter.
  
  - TSLint: https://github.com/palantir/tslint
  - Always use a Linter
  - Our [tslint.json](https://github.com/MBing/typescript_styleguide/blob/master/tslint.json)
  
### Trailing Comma

  - When creating objects or Array or any case of separation, use trailing comma's

  ```typescript
  let person: object = {
    name: 'Stefan',
    home: 'Berlin',
  };
  
  let personTwo: Array<string> = [
      'Chris',
      'Berlin',
  ];
  ```

**[top](#table-of-contents)**


## License
(The MIT License)

Copyright (c) 2017 Contorion, GMBH

This Styleguide is an enhanced & strongly modified version of: [Platypi Typescript Styleguide](https://github.com/Platypi/style_typescript)

Copyright (c) 2014 Platypi, LLC

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the 'Software'), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
