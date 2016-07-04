# The Front End Testing Triforce 

A three-pronged approach for automated testing of front-end applications. 

---

Table of Contents
  - [Part 1: Intro to The Testing Triforce](#Intro to Unit Testing)
    - [link text](#abcd)
    - [else](#else)
  - [Part 2: The Testing Triforce in Practice](#The Triforce in Practice)
  - [Part 3: Additional Benefits of Triforce Development](#Additional Benefits of Triforce Development)
  - [Part 4: Frequently Asked Questions](#FAQ)


-

<div name="Intro to Unit Testing"></div>
## Part 1: Intro to The Testing Triforce
---
### History of The Testing Triforce
The Testing Triforce phrase was coined by Jim Lynch. While working as an angularJS developer he was doing standard unit testing along with some Protractor tests. Jim then read a book on BDD (Behavior Driven Development) and fell in love with the gherkin syntax and the way is was connected to step definitions. It was unclear how exactly to fit this into an Angular, SPA, or general JavaScript project in a way that gelled nicely with the other types of automated tests.  

### Purpose of The Testing Triforce

The testing triforce is meant to prescribe a way for writing three types of automated tests: acceptance tests, e2e tests, and unit tests, but even more than that it builds on the test-first theories of TDD. Thus, the testing triforce becomes a tao, or way of developing software where the result is truly transparent, agile, and well-done.

### Not Angular-Specific
It should be noted that the Testing Triforce is not something that is dependant on the Angular library. It can be applied to really any project made from html, css, and javascript. It can even be applied to other front-end platforms like .NET, Ios, Android, Java, Ruby, C++, etc. For the examples shown here I'm using AngularJS 1.5 in Ecmascript 5. 

### Testing Tooling for Web Applications




## The Triforce

![testing triforce](./images/testing-triforce.png "Testing Triforce")
- credit: the triforce image is a copyrighted symbol of Nintendo Corporation. 

The triforce is a symbol popularized by the video games franchise "The Legend of Zelda".

Here we use it to represent the three types of automated tests that we like to use. 

- Acceptance Tests
- E2e Tests
- Unit Tests

## Acceptance Tests
![cucumber](./images/cucumber.png =50x)![karma](./images/protractor.png "Protractor")![chai-mocha](./images/mocha-chai.png =250x) 

These are tests that come from the theory of behavior-driven development. They consist of two types of files– feature files and step definition files. At ng-nj, we like to use Cucumber.js for this, and we recommend running it through Protractor by selecting the cucumber framework in your protractor.conf.js file. Although these tests are "web tests" and focus on testing the ui in a selenium-like fashion, these tests should use mock data and should NOT be hitting external endpoints. Since these are high level feature specifications tied to low-level step defintions, these tests will cover all of the acceptance criteria for the project.  

<div name="else"></div>
## E2e Tests
![karma](./images/protractor.png "Protractor") ![jasmine](./images/jasmine.png "Jasmine") ![chai-mocha](./images/mocha-chai.png "Chai-Mocha") 

These are tests that do hit external endpoints. Normally, we set these up in a separate protractor.conf.js file. Althoguh we use protractor for these tests, they are not as concerned with simulating an actual user interacting with the application. These tests are solely with interacting with external resources to ensure that they work as expected. 

<div name="abcd"></div>
## Unit Tests

![karma](./images/karma.png "Karma") ![jasmine](./images/jasmine.png "Jasmine") ![chai-mocha](./images/mocha-chai.png "Chai-Mocha") 

Ahh, the unit tests. Incorporating heavy Protractor usage for E2e and acceptance tests should not steal any thunder at all from the classic unit tests. These are concerned with checking individual functions. These normally return a coverage report, and as always we aim for 100% coverage by unit tests. 


<div name="The Triforce in Practice"></div>
## Part 2: The Triforce in Practice
--- 

## Gherkin Comes First


## Implement Step Definitions with Protractor Selenium Tests

## Implement E2e Tests in a Separate Protractor Conf.js file.

## Write the actually code in the usual TDD style with unit tests is code while using the protractor tests and gherkin feature files as a guide for what the code should do.

## Deployment
We recommend a CI pipeline that will automatically run 1) your acceptance tests protrator file, 2) your e2e tests protractor file, and 3) your karma unit tests file. If you don't have a CI server set up, you could always run these three tests manually. The key is that you trust these tests so that they will continue to be run and maintained as the development unfolds. 

### Triforce Tester Certification
If you've been practicing Triforce Testing Development for over a year and would like to try to take the official Triforce Tester Examination for the prestigious "Triforce Tester" designation then simply open an issue on this repo and a proctor will get in touch with you. 


<div name="Additional Benefits of Triforce Development"></div>
## Part 3: Additional Benefits of Triforce Development

## Better Team Communication & Ubiquitous Language

## Living Documentation
Cucumber reposrts, unit test reports, protractor reports(?)

## Planning Specs and Code Always In Sync

<div name="FAQ"></div>
## Part 4: Frequently Asked Questions

There are currently no questions in the FAQ section. PleASe ask a question by submitting an issue.



---

This guide is maintained by ng-nj, the Angular Group of New Jersey.
