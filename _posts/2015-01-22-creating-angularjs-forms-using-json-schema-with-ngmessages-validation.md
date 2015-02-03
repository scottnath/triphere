---
layout: post
date:   2015-01-22 17:00:00
---

# Using a JSON Schema to create AngularJS Forms with ngMessages

Seeking to automate as many things as possible, I now want to add my forms to that automation plan.

## TL;DR

Forms are created using [angular-autofields-bootstrap](https://github.com/JustMaier/angular-autofields-bootstrap) and [ngMessages](https://docs.angularjs.org/api/ngMessages) validation is added in using [AutoField's extensibility system](http://justmaier.github.io/angular-autoFields-bootstrap/#extend).

## Options for Creating AngularJS Form Elements using JSON Schema

These are the three options I found:

* [angular-autofields-bootstrap](https://github.com/JustMaier/angular-autofields-bootstrap)
* [angular-schema-form](https://github.com/Textalk/angular-schema-form)
	* couldn't get [extending options](https://github.com/Textalk/angular-schema-form/blob/master/docs/extending.md) to work
* [angular-formly](https://github.com/formly-js/angular-formly)
	* [basic example](https://github.com/formly-js/angular-formly#example) didn't work

None of these natively use ngMessages.

## ngMessages

Angular-Messages is AngularJS' native way to show validation messages. Here's a couple tutorials that are excellent:

* tutorial: [ode to code: working with validators](http://odetocode.com/blogs/scott/archive/2014/10/16/working-with-validators-and-messages-in-angularjs.aspx)
* tutorial: [year of moo: how to](http://www.yearofmoo.com/2014/05/how-to-use-ngmessages-in-angularjs.html)
	* animation and server-side eval detailed in this one

## Angular AutoFields Bootstrap

I don't use bootstrap, but the bootstrap aspect of AutoFields isn't mandatory so I can use just what I need with autofields.min.js is only 7k.

The extensibility is what's most important, as ngMessages is something I need to add in. AutoFields has [excellent documentation](http://justmaier.github.io/angular-autoFields-bootstrap/#extend) on extending to add new features.

### Support from AutoFields

I was able to [get a response](https://github.com/JustMaier/angular-autoFields-bootstrap/issues/30) from [JustMaier](https://github.com/JustMaier) (the developer) within a day in my request for info. I had worked on my own attempt, but his help was fantastic in getting my ngMessages addon working.

## The Code

### My JSON Schema

```
$scope.schema = [
  { property: 'sso', type: 'text',
    attr: { pattern: '^[0-9]*$', maxlength: 9, minlength: 9, required: true },
    msgs: {
      minlength: 'Needs to have 9 characters',
      pattern: 'Only Numbers in SSO',
      required: 'SSO required'
    },
    validate: false,
    ngMessages: true
  }
];
```

### My AutoFields ngMessages configuration

```
angular.module('autofields.ngMessages', ['autofields.core'])
  .config(['$autofieldsProvider', function($autofieldsProvider){

  // ngMessages support property
  $autofieldsProvider.registerMutator('ngMessages', function(directive, field, fieldElements){
    // check if ngMessages is turned on
    if(!field.ngMessages) return fieldElements;

    // we need to contain ngMessages in it's own form
    var subformName = 'ngMessages'+field.property;
    fieldElements.fieldContainer.attr('ng-form',subformName);
    fieldElements.ngMessages = angular.element('<div/>');
    fieldElements.ngMessages.attr('ng-messages', [subformName,field.property,'$error'].join('.'));
    fieldElements.fieldContainer.append(fieldElements.ngMessages);

    // combine defined messages and default messages
    var allMsg = angular.extend({}, directive.options.validation.defaultMsgs, field.msgs);

    angular.forEach(field.attr, function(value, key){
      if (
        (allMsg && allMsg[key] != null) // allMsg exists and this attribute is among them
        &&
        (field.attr && field.attr[key] != null) // attr exists and this error is in it
      ){
        //Add individual messages for each error
        var ngMessage = angular.element('<div/>');
        ngMessage.attr('ng-message', key);
        ngMessage.html(allMsg[key]);
        fieldElements.ngMessages.append(ngMessage);
      }
    });
    return fieldElements;
  });
}]);
```
