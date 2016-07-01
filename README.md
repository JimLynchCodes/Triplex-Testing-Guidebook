# Understanding the Front End Testing Triforce 

The Front-End testing triforce is a way of thinking about testing applications built on HTML, CSS, and JavaScript. There are many different testing techniques, and at ng-nj we've decided on three core types of testing for our applications. This has been hugely successful for us, and in this document we're sharing our methodologies with the world for those who are interested in automated testing techniques

## Automated Vs Manual Testing


## The Triforce

![testing triforce](./testing-triforce.png "Logo Title Text 1")


The triforce is a symbol popularized by the video games franchise "The Legend of Zelda".

Here we use it to represent the three types of automated tests that we like to use. 

- Acceptance Tests
- E2e Tests
- Unit Tests

## Acceptance Tests

These are tests that come from the theory of behavior-driven development. They consist of two types of files– feature files and step definition files. At ng-nj, we like to use Cucumber.js for this, and we recommend running it through Protractor by selecting the cucumber framework in your protractor.conf.js file. Although these tests are "web tests" and focus on testing the ui in a selenium-like fashion, these tests should use mock data and should NOT be hitting external endpoints. Since these are high level feature specifications tied to low-level step defintions, these tests will cover all of the acceptance criteria for the project.  

## E2e Tests
These are tests that do hit external endpoints. Normally, we set these up in a separate protractor.conf.js file. Althoguh we use protractor for these tests, they are not as concerned with simulating an actual user interacting with the application. These tests are solely with interacting with external resources to ensure that they work as expected. 

## Unit Tests
Ahh, the unit tests. Incorporating heavy Protractor usage for E2e and acceptance tests should not steal any thunder at all from the classic unit tests. These are concerned with checking individual functions. These normally return a coverage report, and as always we aim for 100% coverage by unit tests. 


This guide is maintained by ng-nj, the Angular Group of New Jersey.
