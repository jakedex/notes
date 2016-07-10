# Angular Notes

## [Code School Course](http://campus.codeschool.com/courses/shaping-up-with-angular-js)
* *Directive*: A marker on an HTML tag that tells angular to run or reference some js code
  * e.g. `<html ng-app="store">`
* *Modules*: Where we write pieces of our Angular application, define dependencies of our app
  * e.g. `var app = angular.module('store',  [])`
* *Expressions*: Allow you to insert dynamic values into your HTML

* *Controllers*: Where we define our app's behavior by defining functions and values
  * Wrapping javascript in a closure is a good habit
    ```javascript
    (function(){
      asdfasdf
    })();
    ```

  * `app.controller('StoreController', function(){
      this.product = gem;
    })`
  * `ng-controller="StoreController as store"` -> directive, controller name, alias

### 1.5: Built in Directives

* `ng-show='boolean'` -> show element when true
* `ng-hide`
* `ng-repeat='product in store.products'`

### 2.1: Filters and a new Directive

* `{{ product.price | currency }}` -> gives dollar sign and specifies num of decimals
  * in form, `{{ data : filter:options }} `
  * date, uppercase, limitTo, orderBy,
* use `ng-src` for images

### 2.6: Tabs Inside Out

* `ng-click="tab = 1"`
* Expressions define 2-way data binding, essentially that expressions are re-evaluated when a property changes
* `ng-init="tab = 1"`
* `ng-class="{ active: tab === 1 }"` -> name of the class to set, if true, append class to element

```javascript
app.controller('TabController', function(){
  this.tab = 1;
  this.setTab = function(setTo){
    this.tab = setTo;
  };
  this.isSet = function(tabNum){
    return this.tab === tabNum;
  };
});
```

### 3.1: Forms and Models

* `ng-model` binds the form element to the property (2-way data binding)

### 3.5: Accepting Submissions

* `ReviewController as reviewCtrl`
* `<form ng-submit="reviewCtrl.addReview(product)"`

### 3.8: Form Validations 101

* turn of html validations w/ `<form name="reviewForm" novalidate>`
  * `<select required>` -> `{{ reviewForm.$valid }}`
  * source before typing email `<intput ..... class="ng-pristine ng-invalid"`

### 4.1: Directives

* `ng-include="'project-title.html'"`, expects variable for the name  of the file (string)
* Directives allow you to write HTML that expresses the behavior of your application
* Writing custom Directives
  * Template expanding directives: define custom tag or attr that is to be expanded or replaced
  * Can also express complex UI, call events/register handlers, reuse common components

```javascript
app.directive('elementName', function(){
      return {
        restrict: `E`, (`type of directive, E for html element`)
        templateUrl: 'product-title.html'
      }
  })
```

  * `<element-name>`
  * Also `A` for attribute

### 4.5: Directive Controllers

* Can move controller inside of directive with `controller:`


### 5.3: Services

* Services give your controller additional functionality like:
  * Fetching json with $http
  * logging to console with $log
  * filter an array with $filter

```javascript
var store = this;

store.products = [];

$http.get('/products.json', {apiKey: 'myKey'}).success(function(data){
  store.products = data;
  }
```

* Use with dependency injection

```javascript
app.controller(`ContrName`, ['$http', function($http) {

}]);
```

*
