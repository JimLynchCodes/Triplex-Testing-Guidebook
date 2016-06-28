# Angular 1 Testing Style Guide

The Front-End testing triforce is a way of thinking about testing applications built on HTML, CSS, and JavaScript. There are many different testing techniques, and at ng-nj we've decided on three core types of testing for our applications. This has been hugely successful for us, and in this document we're sharing our methodologies with the world for those who are interested in automated testing techniques

## Automated Vs Manual Testing


## The Triforce

This guide was developed by @webWhizJim and is maintained by ng-nj, the Angular Group of New Jersey.

This is a standardized approach for setting up unit and e2e tests for common situations when developing new featuers in AngularJS.
It is intended to use the same style conventions as the [John Papa Angular 1 Style Guide](https://github.com/johnpapa/angular-styleguide/blob/master/a1/README.md).

This guide is oppinionated in the sense that it assumes you are using our workflow which includes:

- Gulp
- Karma 
- Jasmine
- Proctractor
- ES5 JavaScript
- AngularJS 1.3, 1.4, or 1,5

We reccommend scaffolding from the yeoman generator [Gulp-Angular](https://www.npmjs.com/package/gulp-angular).
