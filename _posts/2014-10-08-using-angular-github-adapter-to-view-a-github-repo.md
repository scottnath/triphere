---
layout: post
date:   2014-10-08 17:00:00
---

# Using Angular Github Adapter to view a GitHub repo

The [Angular Github Adapter](https://github.com/PascalPrecht/angular-github-adapter) creates an AngularJS interface for Michael Aufreiter's [GitHub API javascript wrapper](https://github.com/michael/github). I had a project at work where I wanted to integrate some GitHub api functionality into an AngularJS app and I needed to talk to github.js from AngularJS. This is some example code I used to get details on a GitHub repo.

## Showing Repository Information

The .show() function is inside two promises, so you'll want to chain your thens. The first promise is inside *getRepo*, which calls the *$githubRepository* section of angular-github-adapter.js. The second is in the .show() function itself, which is inside of *$githubRepository*

This basic example is for the public repository for the github.js API wrapper.

```
var viewRepo = angular.module('app', ['pascalprecht.github-adapter']); // Declare dependency of adapter

viewRepo.controller('SiteCtrl', ['$scope', '$github', function($scope, $github) { // adding $github to give access to the $github service
    
  $github.getRepo('michael','github')
    .then(function(result){ // 1st then gets the promise which gives us githubRepository
      return result.show();
    })
    .then(function(repo){ // 'repo' is the result from "return result.show();" above
      console.log(repo); // view the repo object in the console
      $scope.repo = repo; // 'repo' object is now in $scope
    });
}]);
```