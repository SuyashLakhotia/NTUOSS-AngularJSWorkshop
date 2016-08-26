# NTUOSS-AngularJSWorkshop

*by Suyash Lakhotia for NTU Open Source Society*

***Disclaimer*** *- This document is only meant to serve as a reference for the attendees of the workshop. It does not cover all the concepts or implementation details discussed during the actual workshop.*

### Workshop Details:
**When?**: Friday, 26 August 2016. 6:30 PM - 8:30 PM.<br>
**Where?**: Theatre@TheNest, Innovation Centre, Nanyang Technological University<br>
**Who?**: NTU Open Source Society<br>

### Questions?
Raise your hand at any time during the workshop or post your question on the [#tgifhacks](https://ntuoss.slack.com/messages/tgifhacks/) channel on Slack. You can also shoot me an [e-mail](mailto:suyashlakhotia@gmail.com) later.

### Errors?
If you find any mistake (typo or anything else), please make a pull request or [post an issue](https://github.com/SuyashLakhotia/NTUOSS-AngularJSWorkshop/issues/new)! Thanks!<br><br>


## What is AngularJS?
AngularJS is a powerful JavaScript framework built for dynamic web applications. It does this by extending the HTML DOM with additional attributes that make it more responsive to user actions. It also provides developers an easy way to write client-side applications in a clean MVC pattern. AngularJS is completely open source, free and used by thousands of developers around the world. It is currently licensed under the Apache license and maintained by Google.

## Prerequisites
This workshop assumes you have a basic understanding of JavaScript and other common web technologies like the Document Object Model (DOM), HTML, CSS, AJAX etc.

- Download &amp; install a text editor of your choice ([Sublime Text](https://www.sublimetext.com/3), for example).
- Clone this repo on your local system or download the .zip [here](https://github.com/SuyashLakhotia/NTUOSS-AngularJSWorkshop/archive/master.zip) and open it up on your text editor.

## Overview of AngularJS Concepts
Because AngularJS brings with it a lot of new terminology &amp; concepts, it is important that we have a preliminary understanding of a few basic terms listed [here](https://docs.angularjs.org/guide/concepts). Don't worry if you don't understand all of them now as you will encounter these terms in practice as we proceed with the workshop tasks.

## Task 1 - Data Binding
Data binding in AngularJS is the automatic two-way synchronization of data between the model and view components. The way that Angular implements data binding lets you treat the model as the *single-source-of-truth* in your application i.e. the view is a projection of the model at all times. When the model changes, the view reflects the change **and vice-versa**.

Let's create a simple example to demonstrate this. Open up `Task1.html` in your text editor.

**Task1.html**

```html
<!DOCTYPE html>
<html>

    <head>
        <title>Data Binding</title>
        <script type="text/javascript" src="https://ajax.googleapis.com/ajax/libs/angularjs/1.5.8/angular.min.js"></script>
    </head>
    
    <body>
        <div ng-app>
            <h1>Data Binding in AngularJS</h1>
        </div>
    </body>

</html>
```

> Throughout this workshop, we'll be using a CDN to include AngularJS in our HTML files like we've done above inside the `<script>` tag. However, you can alternatively [download the source files](https://angularjs.org) or use a package manager like [Bower](https://bower.io/).

The `ng-app` directive defines where an Angular application is running on our page. In order to bind data to our view, we have to first set up a model for Angular to read data from.

Create a text box inside `<div ng-app>`.

```html
<div ng-app>
    <h1>Data Binding in AngularJS</h1>
    <input type="text" ng-model="message">
</div>
```

The `ng-model` directive tells Angular to bind the value of the input field to a property in the scope object &mdash; `$scope`.

### Binding Using `{{}}`
Now that we have a variable set up, we can bind `message` to our view using the double curly bracket syntax i.e. `{{}}`. Let's bind it to a `<p>` to display it.

```html
<div ng-app>
    <h1>Data Binding in AngularJS</h1>
    <input type="text" ng-model="message">
    <p>{{ message }}</p>
</div>
```

Now, if we start typing into the text field, we can see the text in the `<p>` tag automatically update. What is inside `{{}}` is called an Angular expression, which Angular evaluates and replaces with the result(s). Below are examples of a few more expressions you can plug into a view:

```html
<p>{{ message + message }}</p>
<p>{{ message === 'Hamilton' }}</p>
<p>{{ 2 + 3 }}</p>
```

### Binding Using `ng-bind`
As applications get bigger, it's possible that we see `{{ expression }}` being rendered on the browser for a fraction of a second while Angular is still compiling the template(s). In order to avoid this, an alternative to the `{{}}` syntax is using the `ng-bind` directive.

```html
<div ng-app>
    <h1>Data Binding in AngularJS</h1>
    <input type="text" ng-model="message">
    <p ng-bind="message"></p>
    <p ng-bind="message + message"></p>
    <p ng-bind="message === 'Hamilton'"></p>
    <p ng-bind="2 + 3"></p>
</div>
```

However, a downside to using `ng-bind` is that it replaces the entire inner text of the HTML element. For example, the following two lines serve the same purpose:

```html
<p>You typed: {{ message }}</p>
<p ng-bind="'You typed: ' + message"></p>
```

### One-Time Binding
Even though one of the main benefits of AngularJS is its continuous synchronization of data, this can end up being pretty resource intensive. Thus, one-time binding is useful when displaying data that is static or only needs to be read once from the source. This is achieved by prefixing the variable with `::`.

```html
<div ng-app>
    <h1>Data Binding in AngularJS</h1>
    <input type="text" ng-model="message" ng-init="message = 'Default'">
    <p>{{ message }}</p>
    <p>{{ ::message }}</p>
</div>
```

Here, we have also used the `ng-init` directive to initialize `message` with the value `Default`. `ng-init` is a directive that evaluates the given expression once the DOM element is initialized. However, note that `ng-init` should not be used regularly as scope variables should be initialized in your controller.

## Task 2 - Controllers
In Angular, a controller is defined by a JavaScript constructor function that is used to augment the Angular scope. When a controller is attached to the DOM via the `ng-controller` directive, Angular will instantiate a new controller object using the specified controller's constructor function. A new child scope will be created and made available as an injectable parameter to the controller's constructor function as `$scope`.

The role of controllers in Angular is to expose data to our view via `$scope` (i.e. the view model) &amp; add functions to `$scope` that contain business logic to enhance view behavior. Presentation logic should remain within views and directives.

Open up `Task2.html` & `Task2.js` in your text editor.

**Task2.html**

```html
<!DOCTYPE html>
<html>

    <head>
        <title>Controllers</title>
        <script type="text/javascript" src="https://ajax.googleapis.com/ajax/libs/angularjs/1.5.8/angular.min.js"></script>
        <script type="text/javascript" src="Task2.js"></script>
    </head>

    <body>
        <div ng-app="app">
            <h1>Controllers in AngularJS</h1>
        </div>
    </body>

</html>
```

Like we did in [Task 1](#task-1---data-binding), we create a simple Angular application using `ng-app`. However, we give the attribute a value this time to tell Angular which module to look for when the application *boots up*. In this case, our module's name is `app`.

Let's go ahead and create the module in `Task2.js`.

**Task2.js**

```js
var app = angular.module('app', []);
```

The first parameter in `angular.module()` defines the name of the module while the second parameter is an array of dependencies.

Now, let's create a controller by registering the controller's constructor function to the module.

**Task2.js**

```js
var app = angular.module('app', []);

app.controller('mainCtrl', function($scope) {

});
```

The `module.controller()` function accepts the name of the controller as the first parameter and the controller's constructor function as the second. Angular will pass the child scope as an object i.e. `$scope` to the controller's constructor.

Let's add some data to the `$scope` object which we can then display in our view.

**Task2.js**

```js
var app = angular.module('app', []);

app.controller('mainCtrl', function($scope) {
    $scope.message = 'Hello, NTUOSS!';
});
```

**Task2.html**

```html
<div ng-app="app">
    <h1>Controllers in AngularJS</h1>
    <div ng-controller="mainCtrl">
        <p>{{ message }}</p>
    </div>
</div>
```

In our view, we simply need to attach the controller to the DOM using the `ng-controller` directive and we can subsequently access any property stored in `$scope`.

We can also manipulate the properties stored in `$scope` using custom functions in our controller.

**Task2.js**

```js
var app = angular.module('app', []);

app.controller('mainCtrl', function($scope) {
    $scope.message = 'Hello, NTUOSS';

    $scope.updateMessage = function(newMessage) {
        $scope.message = newMessage;
    };
});
```

**Task2.html**

```html
<div ng-app="app">
    <h1>Controllers in AngularJS</h1>
    <div ng-controller="mainCtrl">
        <p>{{ message }}</p>
        <form ng-submit="updateMessage(newMessage)">
            <input type="text" ng-model="newMessage">
            <button type="submit">Update Message</button>
        </form>
    </div>
</div>
```

The `ng-submit` directive contains an Angular expression that is fired whenever the form is submitted. Now, whenever the user submits the form, the `updateMessage()` function will be called which will update the value of `$scope.message`.

### Controller As Syntax
While everything we've created so far works perfectly, things can get messy when you start nesting controllers, and thus, create nested scopes. This can make it difficult for child scopes to explicitly refer to variables in the parent scope since there is no namespacing.

```html
<div ng-controller="parentCtrl">
    <p>{{ message }}</p>
    <div ng-controller="childCtrl">
        <p>{{ message }}</p>
    </div>
</div>
```

Assuming both `parentCtrl` & `childCtrl` have variables in their scopes named `message`, the inner `<p>` can only refer to `message` in `childCtrl`'s scope.

The solution to this problem is the "controller as" syntax where the controller constructors are coded like we would code a class in JavaScript.

**Task2.js**

```js
var app = angular.module('app', []);

app.controller('mainCtrl', function() {
    var self = this;

    self.message = 'Hello, NTUOSS';

    self.updateMessage = function(newMessage) {
        self.message = newMessage;
    };
});
```

**Task2.html**

```html
<div ng-app="app">
    <h1>Controllers in AngularJS</h1>
    <div ng-controller="mainCtrl as main">
        <p>{{ main.message }}</p>
        <form ng-submit="main.updateMessage(main.newMessage)">
            <input type="text" ng-model="main.newMessage">
            <button type="submit">Update Message</button>
        </form>
    </div>
</div>
```

Using this syntax, we can explicitly refer to a particular controller when we have multiple nested controllers.

## Task 3 - Services
Angular services are substitutable objects that are wired together using dependency injection. They can be used to easily share data & functionality across the app. They are:

- **Lazily Instantiated -** Angular only instantiates a service when an application component depends on it.
- **Singletons -** Each component dependent on a service gets a reference to the single instance generated by the service factory.

Angular offers several useful services (like `$http`), but for most applications you'll also want to create your own.

Let's start with the following code:

**Task3.html**

```html
<!DOCTYPE html>
<html>

  <head>
      <title>Services</title>
      <script type="text/javascript" src="https://ajax.googleapis.com/ajax/libs/angularjs/1.5.8/angular.min.js"></script>
      <script type="text/javascript" src="Task3.js"></script>
  </head>

  <body>
      <div ng-app="app">
          <h1>Services in AngularJS</h1>
      </div>
  </body>

</html>
```

Let's go ahead and create a service to store messages.

**Task3.js**

```js
var app = angular.module('app', []);

app.factory('messages', function() {

});
```

We use the module factory API &mdash; `module.factory()` &mdash; to register a service.

Let's start by returning an empty object from the service. This will be the object that components which depend on this service will receive.

**Task3.js**

```js
var app = angular.module('app', []);

app.factory('messages', function() {
    var messages = {};

    return messages;
});
```

Let's add a couple properties to this object to store the messages & add new messages.

**Task3.js**

```js
var app = angular.module('app', []);

app.('messages', function() {
    var messages = {};

    messages.list = [];

    messages.add = function(message) {
        messages.list.push({id: messages.list.length, text: message});
    };

    return messages;
});
```

Now that our service is ready, let's add a couple controllers to our module to make use of it.

**Task3.js**

```js
app.controller('listCtrl', ['messages', function(messages) {
    var self = this;

    self.messages = messages.list;
}]);
```

**Task3.html**

```html
<div ng-app="app">
    <h1>Services in AngularJS</h1>
    <div ng-controller="listCtrl as list">
        <p ng-repeat="message in list.messages">{{ message.id }}: {{ message.text }}</p>
    </div>
</div>
```

The `ng-repeat` directive iterates over collections in a view, repeating the contents of the element where `ng-repeat` is used.

Let's create another controller &amp; add a form below our list to dynamically add messages to our list.

**Task3.js**

```js
app.controller('addCtrl', ['messages', function(messages) {
    var self = this;

    self.addMessage = function(message) {
        messages.add(message);
    };
}]);
```

**Task3.html**

```html
<div ng-controller="addCtrl as add">
    <form ng-submit="add.addMessage(add.newMessage)">
        <input type="text" ng-model="add.newMessage">
        <button type="submit">Add Message</button>
    </form>
</div>
```

We can also set a default message in the `<input>` and clear the `<input>` when the form is submitted.

**Task3.js**

```js
app.controller('addCtrl', ['messages', function(messages) {
    var self = this;

    self.newMessage = 'Hello, NTUOSS!';

    self.addMessage = function(message) {
        messages.add(message);
        self.newMessage = '';
    };
}]);
```

## Task 4 - Filters
Filters are a simple but powerful tool in Angular. They're primarily used to filter through collections or format values returned by Angular expressions.

Let's start by listing a few names &amp; countries in a simple view using concepts we've just learned.

**Task4.html**

```html
<!DOCTYPE html>
<html>

    <head>
        <title>Filters</title>
        <script type="text/javascript" src="https://ajax.googleapis.com/ajax/libs/angularjs/1.5.8/angular.min.js"></script>
        <script type="text/javascript" src="Task4.js"></script>
    </head>

    <body>
        <div ng-app="app">
            <h1>Filters in AngularJS</h1>
            <div ng-controller="mainCtrl as main">
                <p ng-repeat="person in main.people">
                    {{ person.name }}, {{ person.country }}
                </p>
            </div>
        </div>
    </body>

</html>
```

**Task4.js**

```js
function mainCtrl() {
    var self = this;
    self.people = [{
        name: "Eric Simons",
        country: "USA"
    }, {
        name: "Albert Pai",
        country: "Singapore"
    }, {
        name: "Matthew Greenster",
        country: "Sweden"
    }, {
        name: "Tim Brown",
        country: "USA"
    }, {
        name: "Jake Trump",
        country: "Canada"
    }, {
        name: "Albert Potter",
        country: "Canada"
    }, {
        name: "Bob Dylan",
        country: "USA"
    }, {
        name: "Bernie Sanders",
        country: "Singapore"
    }, {
        name: "Dwayne Johnson",
        country: "USA"
    }, {
        name: "Albert Colbert",
        country: "Germany"
    }];
}

angular.module('app', [])
    .controller('mainCtrl', mainCtrl);
```

### Built-in Filters
Let's start by playing around with a couple built-in Angular filters to filter through our collection &mdash; `people`.

#### `orderBy`
The `orderBy` filter sorts the items in a collection using a particular field.

**Task4.html**

```html
<p ng-repeat="person in main.people | orderBy:'name'">
    {{ person.name }}, {{ person.country }}
</p>
```

The code above will sort the array elements using `name` in ascending order. Using `-name` will sort it in the opposite order.

#### `limitTo`
The `limitTo` filter returns the first `n` results. Using `-n` returns the last `n` results.

**Task4.html**

```html
<p ng-repeat="person in main.people | limitTo:4">
    {{ person.name }}, {{ person.country }}
</p>
```

#### `filter`
`filter` allows for filtering a collection based on a search string.

**Task4.html**

```html
<input type="text" ng-model="search"/>
<p ng-repeat="person in main.people | filter:search">
    {{ person.name }}, {{ person.country }}
</p>
```

By default, this will search all the fields in the `person` object (i.e. `name` & `country`). In order to force it to only search for the string in a particular field, the field name has to be specified in the model like so:

```html
<input type="text" ng-model="search.country"/>
```

### Chaining Filters
Angular filters can be chained together using the same pipe operator &mdash; `|`. The filters are applied sequentially on the results of the previous collection filter.

**Task4.html**

```html
<input type="text" ng-model="search"/>
<p ng-repeat="person in main.people | filter:search | limitTo:2">
    {{ person.name }}
</p>
```

### Custom Filters
You can also define your own custom filters in AngularJS. Let's define one to convert each person's name to uppercase.

**Task4.js**

```js
function mainCtrl() { ... }

function makeUpperCase() {
    return function(item) {
        return item.toUpperCase();
    };
}

angular.module('app', [])
    .filter('makeUpperCase', makeUpperCase)
    .controller('mainCtrl', mainCtrl);
```

**Task4.html**

```html
<p ng-repeat="person in main.people">
    {{ person.name | makeUpperCase}}, {{ person.country }}
</p>
```

We define the filter in `Task4.js` by creating its factory function and registering it to the module using `module.filter()`. It can then be applied to any Angular expression that returns a string like `{{ person.name }}`.


## Task ∞ - Going Forward
In closing, I would just like to say that this workshop definitely does not cover everything that AngularJS has to offer. To learn more about AngularJS, you can check out the links below:

- [http://docs.angularjs.org/](http://docs.angularjs.org/)
- [https://www.coursera.org/learn/angular-js/](https://www.coursera.org/learn/angular-js/)
- [http://ruoyusun.com/2013/05/25/things-i-wish-i-were-told-about-angular-js.html](http://ruoyusun.com/2013/05/25/things-i-wish-i-were-told-about-angular-js.html)
- [http://www.tutorialspoint.com/angularjs/angularjs_overview.htm](http://www.tutorialspoint.com/angularjs/angularjs_overview.htm)
- [https://www.codeschool.com/courses/shaping-up-with-angular-js](https://www.codeschool.com/courses/shaping-up-with-angular-js)
- [https://thinkster.io/a-better-way-to-learn-angularjs](https://thinkster.io/a-better-way-to-learn-angularjs)
- [http://code.tutsplus.com/tutorials/5-awesome-angularjs-features--net-25651](http://code.tutsplus.com/tutorials/5-awesome-angularjs-features--net-25651)

*P.S. There is a [new version of Angular](https://angular.io/) built for mobile &amp; desktop that got out of beta very recently.*