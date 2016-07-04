# The Front End Testing Triforce 

A three-pronged approach for automated testing of front-end applications. 

Table of Contents
  - [link text](#abcd)
  - - [else](#else)
  


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


### Triforce Tester Certification
If you've been practicing Triforce Testing Development for over a year and would like to try to take the official Triforce Tester Examination for the prestigious "Triforce Tester" designation then simply open an issue on this repo and a proctor will get in touch with you. 

### FAQ

Q. 



---

This guide is maintained by ng-nj, the Angular Group of New Jersey.
