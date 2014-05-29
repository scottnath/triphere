# How to add Restangular to a generator-angular-require created app

I needed to add Restangular to my app. These are the steps I followed.

I assume these steps will be similar for adding other third-party libraries and scripts?

## Download Restangular to your app
command line:

```bower install restangular --save-dev```

this downloads both restangular and lodash and adds them to your bower.json file so they can be installed when setting up in other places

## Add Restangular to your ./app/scripts/main.js

```
require.config({
  paths: {
    ...
   'angular-cookies': '../bower_components/angular-cookies/angular-cookies',
    'lodash': '../bower_components/lodash/dist/lodash.min',
    'restangular': '../bower_components/restangular/src/restangular',
    angular: '../bower_components/angular/angular'
  },
  shim: {
    ...
    'restangular': [
      'angular', 'lodash'
    ]
  },
  ...
```

## Add Restangular to your ./app/scripts/app.js