
<img src="./images/cucumber.png" height="50" width="48">

# The Front End Testing Triforce Guide

A three-pronged approach for automated testing of front-end applications. 

---

Table of Contents
  - [Part 1: Intro to The Testing Triforce](#Intro to Unit Testing)
    - [History of the Testing Triforce](#history)
    - [Purpose of The Testing Triforce](#Purpose of The Testing Triforce)
    - [It's Not Specific Angular](#It's Not Specific Angular)
    - [This is a Guide](#This is a Guide)
  - [Part 2: The Three Types of Automated Tests](#The Three Types of Automated Tests)
    - [The Triforce Diagram](#The Triforce Diagram)
    - [Acceptance Tests](#Acceptance Tests)
    - [E2e Tests](#E2e Tests)
    - [Unit Tests](#Unit Tests)
  - [Part 3: The Testing Triforce in Practice](#The Triforce in Practice)
    - [Where Do I Put My Files?](#Where Do I Put My Files)
    - [The Gherkin Comes First](#The Gherkin Comes First)
    - [Implement Step Definitions with Protractor](#Implement Step Definitions with Protractor)
    - [Implement E2e Tests in a Separate Protractor Config file](#Implement E2e Tests in a Separate Protractor Conf.js file)
    - [Write Unit Tests and Code TDD Style](#Write Unit Tests and Code TDD Style)
    - [Deployment](#Deployment)
    - [Testing On Multiple Browsers](#Testing On Multiple Browsers)
    - [Triforce Tester Certification](#Triforce Tester Certification)
  - [Part 4: Additional Benefits of Triforce Development](#Additional Benefits of Triforce Development)
    - [Beter Team COmmunication and Ubiquitous Language](#Beter Team COmmunication and Ubiquitous Language)
    - [The Requirements and Code Are Always In Sync](#The Requirements and Code Are Always In Sync)
    - [Living Documentation](#Living Documentation)
  - [Part 5: Reporting](#Reporting)
    - [Generating Reports From the Codebase](#Generating Reports From the Codebase)
    - [Meetings with "The Boss"](#Meetings with "The Boss")
    - [Sample Reports](#Sample Reports)
  - [Part 6: Frequently Asked Questions](#FAQ)
    - [Q. Why is it wrong to treat low level step definitions like unit tests?](#Q1)
    - [Q. Do I *need* to use acceptance tests?](#Q2)
    - [Q. Do I *need* to use unit tests?](#Q3)
    - [Q. Do I *need* to use e2e tests?](#Q4)
    - [Q. When should I *NOT* use the Testing Triforce?](#Q5)
    - [Q. Most Cucumber / BDD examples have a root level "features" folder. Why don't you follow this convention?](#Q6)


-

<div name="Intro to Unit Testing"></div>
## Part 1: Intro to The Testing Triforce
---
<div name="history"></div>
### History of The Testing Triforce
The Testing Triforce phrase was coined by Jim Lynch. While working as an angularJS developer he was doing standard unit testing along with some Protractor tests. Jim then read a book on BDD (Behavior Driven Development) and fell in love with the gherkin syntax and the way is was connected to step definitions. It was unclear how exactly to fit this into an Angular, SPA, or general JavaScript project in a way that gelled nicely with the other types of automated tests. After intensely studying these types of testing and using the, on various real-world projects he finally [built of time] found a way of developing software that works well and incorporated the three types of automated tests. This document attempts to formalize this philosphy that is now known as The Testing Triforce.

<div name="Purpose of The Testing Triforce"></div>
### Purpose of The Testing Triforce

The testing triforce is meant to prescribe a way for writing three types of automated tests: acceptance tests, e2e tests, and unit tests, but even more than that it builds on the test-first theories of TDD. Thus, the testing triforce becomes a tao, or way of developing software where the result is truly transparent, agile, and well-done. This guide provides a set of instructions for developing with The Triforce Testing mindset, but it is up to you to find the tao on your own.

<div name="It's Not Specific Angular"></div>
### It's Not Specific Angular
It should be noted that the Testing Triforce is not something that is dependant on the Angular library. It can be applied to really any project made from html, css, and javascript which can be tested with Protractor and JavaScript unit testing framework like Jasmine or Chai-Mocha. It can even be applied to other front-end platforms like .NET, Ios, Android, Java, Ruby, C++, etc. although you will need different tooling for that platform than what is discussed here. 

<div name="This is a Guide"></div>
### This is a Guide
This document is meant to be a guide for implementing Triforce testing into your own project. Rather than be taken as gospel, the ideas expressed here are meant to convince you of the benefits of implementing these three types of automated testing. The prescribes methodoligies here have been tried a tested, but you are free to change things in your own case if you find it necessary to do so.

<div name="The Triforce Diagram"></div>
## The Triforce Diagram

![testing triforce](./images/testing-triforce.png "Testing Triforce")
- credit: the triforce image is a copyrighted symbol of Nintendo Corporation. 

The triforce is a symbol popularized by the video games franchise "The Legend of Zelda".

Here we use it to represent the three types of automated tests: 

- Acceptance Tests
- E2e Tests
- Unit Tests

<div name="Acceptance Tests"></div>
## Acceptance Tests

Acceptance tests, at the very top of the triforce, should be the starting point at the beginning of any automated testing effort. Because it necessarily forces you to think about the application in high level terms about what it is actually doing, it is a perfect way to **figure out what you want to build** while at the same time *effectively communicating those ideas to the developers, business analysts, and other stakeholders*. 

The gherkin feature files are normally referred to as high level acceptance tests. Using the Given-When-Then-And-But syntax, these high level acceptance tests are then mapped to low-level acceptance tests, written in your projects main programming language (in this case JavaScript). 

Acceptance tests don't end with the feature files in Gherkin syntax. Acceptance tests refer to both the feature files and the step definition files. These should be basically selenium web-tests. Some people may be inclined to treat the low level step definition methods as if they were unit tests. **Don't fall into this trap.** 




![cucumber](./images/cucumber.png)![karma](./images/protractor.png "Protractor")![chai-mocha](./images/mocha-chai.png =250x) 

These are tests that come from the theory of behavior-driven development. They consist of two types of files– feature files and step definition files. At ng-nj, we like to use Cucumber.js for this, and we recommend running it through Protractor by selecting the cucumber framework in your protractor.conf.js file. Although these tests are "web tests" and focus on testing the ui in a selenium-like fashion, these tests should use mock data and should NOT be hitting external endpoints. Since these are high level feature specifications tied to low-level step defintions, these tests will cover all of the acceptance criteria for the project.  

<div name="E2e Tests"></div>
## E2e Tests
![karma](./images/protractor.png "Protractor") ![jasmine](./images/jasmine.png "Jasmine") ![chai-mocha](./images/mocha-chai.png "Chai-Mocha") 

These are tests that do hit external endpoints. Normally, we set these up in a separate protractor.conf.js file. Althoguh we use protractor for these tests, they are not as concerned with simulating an actual user interacting with the application. These tests are solely with interacting with external resources to ensure that they work as expected. These tests could do such things like check to see if files exist in a remote location, check that any random transaction works for your current database instance, check that saving and retrieving data from the file system works, etc. this is also the place where you might put exploratory tests (tests that try to expose bugs) or other types of stress tests.

<div name="Unit Tests"></div>
## Unit Tests

![karma](./images/karma.png "Karma") ![jasmine](./images/jasmine.png "Jasmine") ![chai-mocha](./images/mocha-chai.png "Chai-Mocha") 

Ahh, the unit tests. Incorporating heavy Protractor usage for E2e and acceptance tests should not steal any thunder at all from the classic unit tests. Indeed, doing all that preparatory Protractor work and writing out the features in gherkin, makes it much easier to start unit testing because you have a clear direction of where you want to be. Unit tests are concerned with checking individual functions. These normally return a coverage report, and as always we aim for 100% coverage by unit tests. 


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
It is truly amazing how much gherkin feature files can bring a team together. 


## Planning Specs and Code Are Always In Sync
One of the really nice things about using gherkin feature files instead of having some external planning software is that with gherkin your plans are always in sync with your tests, and your test are always in sync with your code. Thus, the plans stay in sync with the the code. When you plans are not directly embedded in the code it becomes easy to let the plans become out of date and brush them aside. With gherkin, these plans are executed via the command line and drive the decision for acceptance of the entire codebase. This gives the planning an importance unlike any other methodology, and they necessarily must be maintained, taken seriously, and should be considered as important as any other code for the project. 


## Living Documentation
Cucumber reposrts, unit test reports, protractor reports(?)




<div name="FAQ"></div>
## Part 4: Frequently Asked Questions

There are currently no questions in the FAQ section. PleASe ask a question by submitting an issue.


<div name="Reporting"></div>
## Part 5: Reporting
A lot of programmers qould laugh at someone who told them they needed to create documentation for their code. Documentation takes time to write, quickly becomes out of sync with your code, and is just plan annoying for developers to write. Luckily, Triforce Testing puts tremendous focus on good reporting, since these are just the artifacts of running each set of tests for a given type. 


<div name="Meetings with The Boss"></div>
### Meetings with "The Boss"
The leadership, project sponsors, owners, and bosses of you, the lead developer, want to know periodically that progress is being made towards completion of the project and that there is a clear path for the future ahead. That's perfectly acceptable. This is perfectly illustrated with a cucumber report such as [this one](http://htmlpreview.github.io/?https://github.com/gkushang/grunt-cucumberjs/blob/cucumber-reports/test/cucumber-reports/cucumber-report-bootstrap.html). Once everyone's code is merged the script to generate the cucumber report is run again (or automatically run on your CI server and hosted to an internal url) you can just walk into the meeting with "the boss" with the two of you looking at the cucumber report. Ideally you want to say something like, "Last week we had 20 acceptance tests (aka gherkin scenarios) of 80 passing, 1 failing, and the rest unimplemented. Now week have 30 acceptance tests passing, 0 failing, and the rest unimplemented." Of course of accpetance test may be much for difficult and/ or time consuming to implement thatn another, and that does't really come thropugh too well in this report. However, this report tells you exactly what features were worked on in plain english language and whether it's working right now. If you're dealing with a more technical boss you can go into the actual methods of your code by going to your unit testing report such as this one or even your e2e reports like this one. If you have failing e2e tests that's kind of a bad thing so hopefully your e2e report is relatively boring. This is a great way to convey a ton of information; a complete snapshot of the project's development at any time. You can do this quickly and effectively and then talk about other things related to other coworkers, lunch, golf, etc. The boss can then refer back to these charts at any time after the meeting by visiting each corresponding url.


<div name="#FAQ"></div>
### Frequently Asked Questions
There are currently no questions in the FAQ section. Please ask a question by submitting an issue.




---

This guide is maintained by ng-nj, the Angular Group of New Jersey.
