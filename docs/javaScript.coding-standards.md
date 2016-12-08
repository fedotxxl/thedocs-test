<!-- tags: js, javaScript, angularJs, coding, standards -->

# JS coding standards

## Common JS coding standards
* don't use inline js
* use "" instead of '' (correct: `var a = "hello"`, incorrect: `var b = 'hello'`)
* use camel-case variable names (correct: `var helloWorld;`, incorrect: `var hello_world;`)
* use named functions instead of anonymous ones (correct: `function doSomething() {}`, incorrect: `var doSomething = function() {}`)

## AngularJS specific coding standards
### Angular Style Guide
Please read [Angular Style Guide](https://github.com/johnpapa/angular-styleguide) first.  

* Following rules are required:
[Y001](https://github.com/johnpapa/angular-styleguide#style-y024),
[Y023](https://github.com/johnpapa/angular-styleguide#style-y023),
[Y033](https://github.com/johnpapa/angular-styleguide#style-y033),
[Y034](https://github.com/johnpapa/angular-styleguide#style-y034),
[Y035](https://github.com/johnpapa/angular-styleguide#style-y035),
[Y072](https://github.com/johnpapa/angular-styleguide#style-y072).  
* Following rules should be skipped:
[Y120-Y126](https://github.com/johnpapa/angular-styleguide#style-y120)  
* Other rules should be considered as a good practice.

### Devadmin specific coding standards
* main module should be named "app" and stored into "app.js" file
* common features module (services / directives shared between projects) should be named "common"
* AngularJS service name should start with '_' (this help to distinguish angular service from other variables)
* private variables may contain _ at the end
* AngularJS services (starts with `$`) should be injected before custom services (correct: `$q, _myService`, incorrect: `_myService, $q`)
* most services should be stored into separate "${serviceName}.js" file. This rule may be omitted if services/controllers are strictly coupled together
* do not name files/directories as "controller.js" / services / etc. Instead use filenames which describes it's content (correct: `menu/`, `albums.list.js`, `albums.voting.js`)
* controller name should end with `Controller` (correct: `MyController`, incorrect: `MyCtrl`)
* use `.controller` to declare controllers (correct: `.controller('MyController', function() {})`, incorrect: `function MyController() {}`)
* use correct directories (libs / common app / common shared / page specific)

## AngularJS advices
* remember that your code should be correctly minified by `ng-annotate`
* use one-time binding whenever it's possible

## See more
[JavaScript suggestions](./javaScript-suggestions.md) - general suggestions to make your code better