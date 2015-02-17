---
layout: post
date:   2015-02-17 16:52:45
---

# How to publish Yeoman sub-generators on NPM

I ran into an issue where my sub-generators were not getting published to the NPM registry. I followed the instructions [here](https://docs.npmjs.com/getting-started/publishing-npm-packages) to create a version and publish it, but the sub-generators didn't get published.

I googled forever, then finally found [this StackOverflow thread](http://stackoverflow.com/questions/22855656/yeoman-generator-does-not-include-subgenerator-after-publishing-to-npm) which mentioned the package.json files array, which, if you don't add your sub-generator folders to that list, they do not get published to the NPM registry. Fun!

Note: I never saw this mentioned in any Yeoman generator how-to articles. js

## Option 1: Add to package.json files array

find this section:

```
"files":[
    "app"
],
```

and add your sub-generator's folder like so:

```
"files":[
    "app",
    "subgen1",
    "subgen2"
],
```

## Option 2: Remove files array from package.json

find this section:

```
"files":[
    "app"
],
```

delete it because it sucks.