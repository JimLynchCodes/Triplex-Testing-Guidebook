
# <img src="./images/nice-triforce.png" height="30"> ~ The Triplex Testing Guidebook ~ <img src="./images/nice-triforce.png" height="30">

*Official tagline: li
A three-pronged approach to building great software with automated tests.*

*Less trendy, but more descriptive tagline: 
A methodology for leveraging automated acceptance, e2e, and unit tests to build great front-end applications (especially with JavaScript and SPA frameworks such as Angular).*

---

Table of Contents
  - [Part 1: Intro to The Testing Triplex](#Intro to The Testing Triplex)
    - [History of the Testing Triplex](#history)
    - [Purpose of The Testing Triplex](#Purpose of The Testing Triplex)
    - [It's Not Specific To Angular](#It's Not Specific To Angular)
    - [This is a Guide for Developing Software](#This is a Guide)
    - [Is This Yet Another Interpretation of "Agile"?](#Is This Yet Another Interpretation of Agile?)
    - [Perfect Code Over Time Is Attainable](#Perfect Code Over Time Is Attainable)
  - [Part 2: The Three Types of Automated Tests](#The Three Types of Automated Tests)
    - [Overview of the Three Parts](#Overview of the Three Parts)
    - [The Triplex Diagram](#The Triplex Diagram)
    - [Acceptance Tests](#Acceptance Tests)
      - A Gherkin Example
      - A Step Definition Example
      - Running Acceptance Tests
    - [E2e Tests](#E2e Tests)
      - An E2e Test Example
      - Running E2e Tests
    - [Unit Tests](#Unit Tests)
      - A Unit Test Example
      - Running Unit Tests
  - [Part 3: The Testing Triplex in Practice](#The Triplex in Practice)
    - [Where Do I Put My Files?](#Where Do I Put My Files)
    - [The Gherkin Comes First](#The Gherkin Comes First)
    - [Executing The Gherkin Scripts](#Executing The Gherkin Scripts)
    - [Executing the Acceptance Tests](#Executing the Acceptance Tests)
    - [Implementing Step Definitions as Web Tests](#Implementing Step Definitions as Web Tests)
    - [Implementing Step Definitions as Unit Tests](#Implementing Step Definitions as Unit Tests)
    - [Avoiding the UI in Step Definitions](#Avoiding the UI in Step Definitions)
    - [Implementing E2e Tests in a Separate Protractor Config file](#Implementing E2e Tests in a Separate Protractor Conf.js file)
    - [Write Unit Tests and Code TDD Style](#Write Unit Tests and Code TDD Style)
    - [All the Browsers in All the Land](#All the Browsers in All the Land)
    - [Notes on Deployment](#Deployment)
    - [Testing On Multiple Browsers](#Testing On Multiple Browsers)
    - [Everyone Reads the Gherkin, Dev's Change the Gherkin](#Everyone Reads, Devs Change)
    - [No Manual Testers](#No Manual Testers)
    - [The BAU Handoff](#The BAU Handoff)
  - [Part 4: Additional Benefits of Triplex Development](#Additional Benefits of Triplex Development)
    - [Better Team Communication and Ubiquitous Language](#Better Team Communication and Ubiquitous Language)
    - [The Requirements and Code Are Always In Sync](#The Requirements and Code Are Always In Sync)
    - [No Manual Testing](#No Manual Testing)
    - [Living Documentation](#Living Documentation)
  - [Part 5: Reporting](#Reporting)
    - [Generating Reports From the Codebase](#Generating Reports From the Codebase)
    - [Meetings with "The Boss"](#Meetings with The Boss)
    - [Sample Reports](#Sample Reports)
  - [Part 6: Official Triplex Projects](#Official Triplex Projects)
    - [NG-NJ](#NG-NJ)
  - [Part 7: Closing Thoughts](#Closing Thoughts)
    - [The Mythical "Fourth Plex"](#The Mythical Fourth Plex)
    - [Laid Back Perfectionism](#Laid Back Perfectionism)
    - [Why "Test Your Own Code" Is a Terrible Policy](#Why Test Your Own Code Is a Terrible Policy)
    - [Triplex Testing and the V-Model](#Triplex Testing and the V-Model)
    - [Effective Collaboration and Mob Programming](#Effective Collaboration and Mob Programming)
    - [Exploratory Testing](#Exploratory Testing)
    - [Triplex Testing Community Groups](#Triplex Testing Community Groups)
    - [The Jasmine Vs. Chai Debate](#The Jasmine Vs. Chai Debate)
    - [The Importance of Having Conversations](#The Importance of Having Conversations)
    - [Triplex Tester Certification](#Triplex Tester Certification)
  - [Part 8: Frequently Asked Questions](#FAQ)
    - [Q1. Is it wrong to treat low level step definitions like unit tests?](#Q1)
    - [Q2. Do I *need* to use acceptance tests?](#Q2)
    - [Q3. Do I *need* to use unit tests?](#Q3)
    - [Q4. Do I *need* to use e2e tests?](#Q4)
    - [Q5. When should I *NOT* use the Testing Triplex?](#Q5)
    - [Q6. Most Cucumber / BDD examples have a root level "features" folder. Why don't you follow this convention?](#Q6)
    - [Q7. My boss says we don't have enough time for testing. What should I do?](#Q7)
    - [Q8. Q8. Can't we just manually test everything?](#Q8)
    - [Q9. Will the theory of Triplex Testing work for [insert favorite platform here]?](#Q9)


<div name="Intro to The Testing Triplex"></div>
## Part 1: Intro to The Testing Triplex
---
<div name="history"></div>
### History of The Testing Triplex
The Testing Triplex phrase was coined by Jim Lynch. While working as an angularJS developer he was doing standard unit testing along with some Protractor tests. Jim then read a book on BDD (Behavior Driven Development) and fell in love with the gherkin syntax and the way is was connected to step definitions. It was unclear how exactly to fit this into an Angular, SPA, or general JavaScript project in a way that gelled nicely with the other types of automated tests. After intensely studying these types of testing and using the, on various real-world projects he finally [built of time] found a way of developing software that works well and incorporated the three types of automated tests. This document attempts to formalize this philosphy that is now known as The Testing Triplex.

<div name="Purpose of The Testing Triplex"></div>
### Purpose of The Testing Triplex

The testing triplex is meant to prescribe a way for writing three types of automated tests: acceptance tests, e2e tests, and unit tests, but even more than that it builds on the test-first theories of TDD. Thus, the testing triplex becomes a tao, or way of developing software where the result is truly transparent, agile, and well-done. This guide provides a set of instructions for developing with The Triplex Testing mindset, but it is up to you to find the tao on your own.

<div name="It's Not Specific To Angular"></div>
### It's Not Specific To Angular
It should be noted that the Testing Triplex is not something that is dependant on the Angular library. It can be applied to really any project made from html, css, and javascript which can be tested with Protractor and JavaScript unit testing framework like Jasmine or Chai-Mocha. It can even be applied to other front-end platforms like .NET, Ios, Android, Java, Ruby, C++, etc. although you will need different tooling for that platform than what is discussed here. 

<div name="This is a Guide"></div>
### This is a Guide For Developing Great Software
This document is meant to be a guide for implementing triplex testing into your own project. Rather than be taken as gospel, the ideas expressed here are meant to convince you of the benefits of implementing these three types of automated testing. The prescribes methodoligies here have been tried a tested, but you are free to change things in your own case if you find it necessary to do so. Note that this is not a guide for writing or running any of the three test types (although you may find the sample config files and shell commands useful). Rather, this is a more meta guide on building great software by leveraging automated testing. 
 
 <div name="Is This Yet Another Interpretation of Agile?"></div>
### Is This Yet Another Interpretation of "Agile"?
This question here is whether Triplex Testing is really just another interpretation of "Agile methodologies". In some ways, yes. Triplex Testing values many of the core agile principles, but I like to think that Triplex Testing is a bit more description about *how* you acutally go about working this way from a programming point of view. In fact, Triplex Testing is so focused on the technical aspects that I would recommend any team attempting to try this to also look into [Design Driven Devlopment](#http://www.designdrivendevelopment.org/) and [Agile Project Management](#https://www.mountaingoatsoftware.com/agile/agile-project-management) since, while we think these are important, they are not covered in this guidebook. It seems that everyone has their own personal version of what agile means to them. We consider Triplex Testing to be a methodology that overlaps with Agile in that it values things like extreme programming, automated testing, continuous integration / deployment, plenty of communication among stakeholders, pair / mob programming, adaptive and interative cycles, and heavy customer / user involvement.
 
---
 <div name="Perfect Code Over Time Is Attainable"></div>
### Perfect Code Over Time Is Attainable
Software is an interesting thing in that it needs to be 100% perfect or else it doesn't work, everything breaks, and the users are disgusted! Because of this level of perfection that is inherently needed, it would be wise to treat any software project that plans to go into production as if it were a NASA project, and if it were the government itself of something country. What I'm trying to get at here is that there needs to be a series of checks and balances in place so that it is virtually impossible for all the tests to be passing and have something wrong. *And when some bug IS discovered* or a new featuer is requested Triplex Testing gives us a clear path of 1. setting up gherkin feature files, 2.implementing the step definitions, 3. implementing and e2e tests, and 4. writing unit tests along with the production code. I'll discuss more in later sections what exactly I mean by *perfect code*, but just know that without a solid suite of automated tests it will be an **extremely challenging, stressful, burdensome journey with horrific surprises, frustration pain.** You might get lucky and put something out once that works, but if you want to be a nimble dev team that moves fast then sooner of later you will slip and push a bug without tests. As software is an all-or-nothing deal, pushing bugs is devestating and could potentially ruin your product, brand, and business. If you want to be a wild cowboy coder with no tests, do it on your side projects. *For code that's going into production, use Triplex Testing!*        


---

 <div name="The Three Types of Automated Tests"></div>
## Part 2: The Three Types of Automated Tests


 <div name="Overview of the Three Parts"></div>
### Overview of the Three Parts
If you looked up the word *triplex* in the dictionary you would get such definitions like, "a dwelling composed of three units" or, "having three parts". Triplex Testing gets it name from it's three independent parts, and understanding each of the three parts is critical to doing Triplex Testing correctly. Later in this chapter we'll get more technical and later we'll talk about different tooling for various tests, but here I want to describe each of the three parts in simple, platform-independent terms.

- Tests that check the **requirements, behavior, specifications** of the project. 


- Tests that check the **internal application logic and algorithms** of the project  - 


- Tests that check the **interactions and connections between components or systems**. 


<div name="The Triplex Diagram"></div>
### The Triplex Diagram

![testing triplex](./images/testing-triforce.png "Testing Triplex")

*credit: the triforce image is a copyrighted symbol of Nintendo Corporation and was popularized by the video games franchise "The Legend of Zelda".*

Here we use it the triplex diagram represent the three types of automated tests: 

- Acceptance Tests
- E2e Tests
- Unit Tests

<div name="Acceptance Tests"></div>
### Acceptance Tests
<img src="./images/cucumber.png" height="47"><img src="./images/protractor.png" height="50"> <img src="./images/mocha-chai.png" height="50">

Acceptance tests, at the very top of the triplex diagram, should be the starting point at the beginning of any automated testing effort. Because it necessarily forces you to think about the application in high level terms about what it is actually doing, it is a perfect way to **figure out what you want to build** while at the same time *effectively communicating those ideas to the developers, business analysts, and other stakeholders*. 

The gherkin feature files are normally referred to as high level acceptance tests. Using the Given-When-Then-And-But syntax, these high level acceptance tests are then mapped to low-level acceptance tests, written in your projects main programming language (in this case JavaScript). 

Acceptance tests don't end with the feature files in Gherkin syntax. Acceptance tests refer to both the feature files and the step definition files. These should be basically selenium web-tests. Some people may be inclined to treat the low level step definition methods as if they were unit tests. **Don't fall into this trap.** 


These are tests that come from the theory of behavior-driven development. They consist of two types of files– feature files and step definition files. At ng-nj, we like to use Cucumber.js for this, and we recommend running it through Protractor by selecting the cucumber framework in your protractor.conf.js file. Although these tests are "web tests" and focus on testing the ui in a selenium-like fashion, these tests should use mock data and should NOT be hitting external endpoints. Since these are high level feature specifications tied to low-level step defintions, these tests will cover all of the acceptance criteria for the project.  

<div name="E2e Tests"></div>
### E2e Tests
<img src="./images/karma.png" height="50"><img src="./images/protractor.png" height="50"> <img src="./images/mocha-chai.png" height="50">

These are tests that do hit external endpoints. Normally, we set these up in a separate protractor.conf.js file. Althoguh we use protractor for these tests, they are not as concerned with simulating an actual user interacting with the application. These tests are solely with interacting with external resources to ensure that they work as expected. These tests could do such things like check to see if files exist in a remote location, check that any random transaction works for your current database instance, check that saving and retrieving data from the file system works, etc. this is also the place where you might put exploratory tests (tests that try to expose bugs) or other types of stress tests.

<div name="Unit Tests"></div>
### Unit Tests
<img src="./images/karma.png" height="47"><img src="./images/jasmine.png" height="50"> <img src="./images/mocha-chai.png" height="50">

Ahh, the unit tests. Incorporating heavy Protractor usage for E2e and acceptance tests should not steal any thunder at all from the classic unit tests. Indeed, doing all that preparatory Protractor work and writing out the features in gherkin, makes it much easier to start unit testing because you have a clear direction of where you want to be. Unit tests are concerned with checking individual functions. These normally return a coverage report, and as always we aim for 100% coverage by unit tests. 


--- 
<div name="The Triplex in Practice"></div>
## Part 3: The Triplex in Practice
This section provides some advice for using the Triplex in Practice.

<div name="Where Do I Put My Files"></div>
### Where Do I Put My Files? 
Most experienced SPA developers agree that at a high level a feature-based directory structure scales best and that parallel directory structures should be avoided. Tests that can be directly attributedto certain classes or features should be near them. We recommend putting a *feature* directory in the root directory of that particular feature. Then put the .feature file and step definitions (optionally in a step_definitions subfolder) inside of the new directory. For units tests I like to keep the .spec.js test file directly next to the correponsing .js file. Since our acceptance tests are the selenium / Protractor tests heavily tied to the features, the E2e tests can be more general. For example, an e2e test could just check that a database endpoint returns *something.* This has nothing to do with any particular feature, and for this reason it's customary to have an e2e folder on the same level as the src folder which stores all of the e2e tests. In JavaScript a good build script can sort out the feature and step definition files so it's fine to put your acceptance tests and unit tests right in the src folder with the relevant files for that particular feature. As a final note on this topic I'll mention that if you do decide to have *parallel directory trees* and your apps grows large enough you (or your developers) are going to be scrolling like crazy, losing track of files, and possibly considering giving up on testing. Make good choices about your directory structure.                                 

<div name="The Gherkin Comes First"></div>
### Gherkin Comes First
Is a piece of software really anything more than the features it provides? What better way to begin describing a project than by describing gherkin features and scenarios? And if we are discussing them, we might as well write them into .feature files because then they can be stored in version control, referred back to later, and even executed by command shell. Here's an example of some Gherkin **code**:
```
Feature: Display Weather
    In order to see the current temperature on the screen
    As a user of the app
    I want to see the weather on the screen wehn the page loads.

    Scenario: Page first loads
      Given I navigate to this page
      When the page first loads
      Then I should see the current temperature displayed.
```

Looks like plan English right? That's the beauty of it. If you start thinking about the vision you have of your application in terms of features and scenarios it help in a number of ways:

- It fleshes out many of situations, and a lot of unknowns and what would be questions down the road are hammered out early. 
- Because it's written down it's not just in one person's head or spoken aloud in a meeting and forgotten. This also makes it clear when two people have different interpretations of something (usually) and helps to clear up understanding.
- Because it's Gherkin syntax, these scenarios can be *executed* to ensure they always pass for the latest build.
- It gives some type of benchmark for progress on the project, scope and timeline estimation, and exposes potentially difficult issues to solve early.


<div name="Executing The Gherkin Scripts"></div>
### Executing The Gherkin Scripts
We recommend running your gherkin JavaScript files through Protractor by setting the framework to "".
Here is an example of a protractor config file that runs the cucumberjs framework:

*acceptance-tests.config.js*
```
'use strict';

exports.config = {
  // The address of a running selenium server.
  // seleniumAddress: 'http://localhost:4444/wd/hub',
  //seleniumServerJar: deprecated, this should be set on node_modules/protractor/config.json

  framework: 'custom',
  frameworkPath: require.resolve('protractor-cucumber-framework'),

  capabilities: {
    'browserName': 'chrome'
  },
  
  resultJsonOutputFile: 'cucumber-report/report-output.txt',

  baseUrl: 'http://localhost:3000',

  specs: [paths.features + 'src/**/*.feature'],

  cucumberOpts: {
    format: 'pretty',
    require: 'src/**/*.step.js'
  },

  jasmineNodeOpts: {
    defaultTimeoutInterval: 25000
    //   showColors: true,
  }

};

```

<div name="Executing the Acceptance Tests"></div>
### Executing the Acceptance Tests
The ability to run the acceptance tests through the command line is what sets apart Gherkin from just typing out requirements and user stories into Jira or Trello. Although vitally important to the triplex testing process, executing your feature files is actually not that hard. 

Add this file to your project and then install the necessary modules

` npm install protractor-cucumber-framework --save-dev`

Now you should be able to run gherkin tests like this:
`./node_modules/protractor/bin/protractor acceptance-tests.config.js`

<div name="Implementing Step Definitions as Web Tests"></div>
### Implementing Step Definitions as Web Tests
If you are using the protractor config file above then you might notice that for the step definition files it's only looking for .steps.js files. This means we can put them anywhere in our project, and we don't need any *step_definitions* folders (but if you think it makes things more readable go ahead and use them). The scenarios will almost always be from a user's point of view, and so it naturally follows to automate the tests from the user's point of view. This is why we write low level step definitions with protractor api. Your scenarios should just describe things that should happen, and in the protractor tests you can *expect* those things to happen after clicking (or interacting with in another way) some element on the page. Also, notice that these tests are still using the underlying functions of the application and so the protractor tests are indirectly testing individual functions of the application. However, because this protractor tests check the application in a *black box* fashion, when errors fail it's tough to find the root cause of issues from these tests alone. 

<div name="Implementing Step Definitions as Unit Tests"></div>
### Implementing Step Definitions as Unit Tests
While using protractor to interact with your page can feel pretty awesome and empowering, don't think that you *have* to write every step definition as a web test. In your *given* statement instead of calling browser.get('./index); we could jsut as well use mocha and angular-mocks and the **inject** keyword to get a reference to our angular objects () in a vacuum. This has the advantage of running a little faster so definitely consider using these instead of web tests when you can. 

<div name="Avoiding the UI in Step Definitions"></div>
### Avoiding the UI in Step Definitions
As mentioned above in "Implementing Step Definitions as Unit Tests", your tests will run faster if they are set up as unit tests instead of web tests. What do industry experts think about this? Here is an [article by Martin Fowler](#http://martinfowler.com/bliki/TestPyramid.html) where he endoreses the *Test Pyramid*, an automated testing concept which recognises the importance of web tests (or ui tests as he calls them) but recommends that you have proportionately more unit tests. In [this podcast episode](#https://cucumber.io/blog/2016/05/09/cucumber-antipatterns) by the folks at CucumberBDD they describe "too many web tests" or "only web tests" as an anti-pattern. They also note this good rule of thumb: *never have scenario outlines that are web tests.* The Scenario outlines are normally meant for different situations or business outcomes. You can have one (or even more than one) web test to make sure the right thing on the page is updating. Then illustrate each example in a unit test step definition in a scenario outline to ensure the calculations or business logic. turn out at they should. 

<div name="Implementing E2e Tests in a Separate Protractor Conf.js file"></div>
### Implementing E2e Tests in a Separate Protractor Conf.js file.
This section is purposely put before "write the production code" because it should come first. Unless you have a really hazy idea of what you're building (red flag), you should at least know what external resources you are connecing to. Even if the backend has not been finished yet, you can still set up the e2e test firing away at it from day one, and simply let it fail. Comment it out if it bothers you, and then as soon as that endpoint is ready add that e2e test back in. Some developers get flustered and afraid when they think about writing e2e tests, but actually these are the easiest of all.

Here is a sample protractor file for running e2e tests:

*e2e-tests.config.js*
```
'use strict';

exports.config = {
  //seleniumAddress: 'http://localhost:4444/wd/hub',
  //seleniumServerJar: deprecated, this should be set on node_modules/protractor/config.json

  capabilities: {
    'browserName': 'chrome'
  },
  
  resultJsonOutputFile: 'e2e/e2e-report.json',

  baseUrl: 'http://localhost:3000',

  specs: ['src/**/*.js'],

  jasmineNodeOpts: {
   showColors: false,
    defaultTimeoutInterval: 30000
  }
};
```

You can run this with this command:
`./node_modules/protractor/bin/protractor e2e-tests.config.js`

<div name="Write Unit Tests and Code TDD Style"></div>
### Write Unit Tests and Code TDD Style 
Write the actually code in the usual TDD style with unit tests is code while using the protractor tests and gherkin feature files as a guide for what the code should do. For modern JavaScript development, karma seems to have gained a stronghold as the most popular unit test runner. Many scaffolded pojects have support for unit testing out of the box, but they are really just providing you with a karma.conf.js file. You could make this file yourself or change your current one as you like. 

Here is an example of a karma configuration file:

*unit-tests.config.js*
```
module.exports = function(config) {

  var configuration = {
    files: listFiles(),

    singleRun: true,

    autoWatch: false,

    ngHtml2JsPreprocessor: {
      stripPrefix: conf.paths.src + '/',
      moduleName: 'icpComp'
    },

    logLevel: 'WARN',

    frameworks: ['phantomjs-shim', 'jasmine', 'angular-filesort'],

    angularFilesort: {
      whitelist: [path.join(conf.paths.src, '/**/!(*.html|*.spec|*.mock).js')]
    },

    browsers : ['PhantomJS'],

    plugins : [
      'karma-phantomjs-launcher',
      'karma-angular-filesort',
      'karma-phantomjs-shim',
      'karma-coverage',
      'karma-jasmine',
      'karma-ng-html2js-preprocessor'
    ],

    coverageReporter: {
      type : 'html',
      dir : 'coverage/'
    },

    reporters: ['progress'],

    proxies: {
      '/assets/': path.join('/base/', conf.paths.src, '/assets/')
    }
  };

  configuration.preprocessors = {};
  pathSrcHtml.forEach(function(path) {
    configuration.preprocessors[path] = ['ng-html2js'];
  });

  config.set(configuration);
};

```

Don't forget to install karma:
`npm install karma --save-dev`

And then run it like this:
`karma start unit-tests.config.js`

You can put .spec.js files anywhere in the src/ folder and they will automatically be picked up when you run karma. 


<div name="All the Browsers in All the Land"></div>
### All the Browsers in All the Land
All the Browsers in All the Land
One amazing tool that is available to you is Sauce Labs. This is a service that you can hook into right from your configuration files that allows you to run your tests on your application code while running on a plethora of different browsers and environments (over 600)! 


<div name="Deployment"></div>
### Notes on Deployment
We recommend a CI pipeline that will automatically run 1) your acceptance tests protrator file, 2) your e2e tests protractor file, and 3) your karma unit tests file. If you don't have a CI server set up, you could always run these three tests manually. The key is that you trust these tests so that they will continue to be run and maintained as the development unfolds. 

<div name="Testing On Multiple Browsers"></div>
### Testing On Multiple Browsers
One key advantage of automated browser testing in that we can take the script we've developed locally and execute it on virtually *any* browser, and we can even do multiple browsers simultaneously. The for-profit company *Sauce Labs* basically runs the show in this area, and connecting to Sauce is even built into the api of Protractor! Simply update your protractor config file with this block to the service instead of running the Protractor tests manually *(note: you will need your replace the constants with your own Sauce Labs credentials)*:

```
if (process.env.TRAVIS) {
  config.sauceUser = process.env.SAUCE_USERNAME;
  config.sauceKey = process.env.SAUCE_ACCESS_KEY;
  config.capabilities = {
    'browserName': 'chrome',
    'tunnel-identifier': process.env.TRAVIS_JOB_NUMBER,
    'build': process.env.TRAVIS_BUILD_NUMBER
  };
 }
```

<div name="Everyone Reads, Devs Change"></div>
### Everyone Reads the Gherkin, Dev's Change the Gherkin
Because the feature files are somewhat scattered around the project's directory structure it can be a little overwhelming for a non-developer to pull the project repo just to read the feature files. The key is to keep the feature files easily readable and accessible by all. Therefore, all non-programmers should be referring to the cucumber reports that are automatically generated. These will show all of the features and scenarios in a nice, collapsable format. If they wish to chhange something it should be discussing with the programmers who then make a change to the feature file in question and push that up to the git repository which then updates the hosted cucumber reports.

<div name="No Manual Testers"></div>
### No Manual Testers
Too often large development companies have qa teams that are just squads of manual testers. Manual testing should be though of as the enemy and avoided. Almsot anything worth testing manually can and should be automated with Protractor. Sometimes, exploratory tests may be useful for pointing out otherwise hard to find bugs, but even then you'll want to automate those tests to check them for regression later. If you currently have manual testers, teach them the ways of Protractor so that can contribute to the automated testing effort. 


<div name="The BAU Handoff"></div>
### The BAU Handoff
Let's be honest. Teams that can practice Triplex Testing well and can build perfect software quickly are best utlized to do just that- *to build.* At some point in any project (possibly years after it has been started), at some point there are no more bugs to fix and no more features to add. However, we cannot just completely abandon our software out in the wild. Things change and break and need to maintained, and *somebody* needs to do it. These developers are referred to as the *Business As Usual*, or BAU, team. The [agile manifesto](#) clearly values, "Working software over comprehensive documentation". The great thing about Triplex Testing is that you need to focus only on working software (and writing working test code). By the automated generation of reports, especially the cucumber reports, the BAU team has available to them a very comprehensive and easy to read for of ducomentation for what the code should do! I also recommend writing a relatively detailed README file for each project, at the very least describing how the project was scaffolded and what task runner scripts are available.

---

<div name="Additional Benefits of Triplex Development"></div>
## Part 4: Additional Benefits of Triplex Development

<div name="Better Team Communication and Ubiquitous Language"></div>
### Better Team Communication and Ubiquitous Language
It is truly amazing how much gherkin feature files can bring a team together. The Given-When-Then-And-But syntax is excellent for describing scenarios and conveying what the software is acutally supposed to accomplish without being concerned with how it is implemented. Having the visual reports to refer to are extremely helpful to all the non-programmers who often have trouble figuring out what's been done already, what's in progess, and what's still on the back burner. 

<div name="The Requirements and Code Are Always In Sync"></div>
### The Requirements and Code Are Always In Sync
One of the really nice things about using gherkin feature files instead of having some external planning software is that with gherkin your plans are always in sync with your tests, and your test are always in sync with your code. Thus, the plans stay in sync with the the code. When you plans are not directly embedded in the code it becomes easy to let the plans become out of date and brush them aside. With gherkin, these plans are executed via the command line and drive the decision for acceptance of the entire codebase. This gives the planning an importance unlike any other methodology, and they necessarily must be maintained, taken seriously, and should be considered as important as any other code for the project. 

<div name="No Manual Testing"></div>
### No Manual Testing
Manual testing can be a huge drain on time and resources. Of course you may not remove manual testing *entirely*, but not having a whole QA team of manual testers and shortening the QA time can be hugely beneficial to an organization in terms of saving potentislly burned cash and being more nimble with changes, bug fixes, and releases. In general, whenever you see an opportunity for manual testing instead try to write an automated test for it. 

<div name="Living Documentation"></div>
### Living Documentation
The Living Documentation that is generaeted by your test runners is the key to the success of BDD. This article defines it well when it describes Living Documentation as, *"a dynamic method of system documentation that provides information that is current, accurate and easy to understand".* 3 Your cucumber tests and e2e tests generate json output that can be viewed by the html and css of your reports. With Istanbul (or similar code coverae tools for non-JavaScript projects) you have living documentation for your unit tests as well. Great documentation served up nicely on a web page; you can have it without ever having to write it! I know it sounds like a dream, but it's not. Leveraging the reports as much as possible to make high level decisions is key to BDD, and help tremendously in the long run. If you're just adopting Triplex Testing remember that generating and reading these three reports is **critical**. If you're an old pro, think back to projects where you didn't have them and remember not to take them for granted!

---
<div name="Reporting"></div>
## Part 5: Reporting
The type of reports we recommend in Triplex Testing are *generated* from the code, specifically from the terst runners. These runners will output information about each test, it's name, all the code it, whether it's passing or failing, etc. into a json object. Many open-source and private report templates have been developed to view and even interact with the json output. The report html and css are just static files that act as a shell or skeleton which you point to your json output file.

<div name="Generating Reports From the Codebase"></div>
### Generating Reports From the Codebase
Generating the json from your test runners is relatively straightforward. When running protractor (for our cucumber / acceptance and e2e tests) we can specify this option in the protractor configuration file:

*(Snippet from protractor-acceptance.conf.js)*
```
 resultJsonOutputFile: 'acceptance-reports/acceptance-report-data.json',
```

This will recreate and overwrite the file *acceptance-report-data.json* each time the tests are run. For units tests I recommend using Istanbul and running the tests with Karma. In your karma configuration file you can set similar settings for the location where you want the reports files to be placed.

*(Snippet from karma.conf.js)*
```
 plugins : [
      'karma-phantomjs-launcher',
      'karma-angular-filesort',
      'karma-coverage',
      'karma-jasmine',
      'karma-ng-html2js-preprocessor'
    ],

    coverageReporter: {
      type : 'html',
      dir : 'coverage/'
    },
```

The key thing to realize is that the developers never need to stop what they are doing to "work on documentation". They can focus solely on writing good tests and making them pass, but at any time anyone can stop and look at the current progress and road ahead by these automatically generated reports. This is therefore extremely efficient, and because of it's level of detail and sleek interface the reports provide a tremendously valuable communication tool for stakteholders and developers to all work together to build the perfect product.


<div name="Meetings with The Boss"></div>
### Meetings with "The Boss"
The leadership, project sponsors, owners, and bosses of you, the lead developer, want to know periodically that progress is being made towards completion of the project and that there is a clear path for the future ahead. That's perfectly acceptable. This is perfectly illustrated with a cucumber report such as [this one](http://htmlpreview.github.io/?https://github.com/gkushang/grunt-cucumberjs/blob/cucumber-reports/test/cucumber-reports/cucumber-report-bootstrap.html). Once everyone's code is merged the script to generate the cucumber report is run again (or automatically run on your CI server and hosted to an internal url) you can just walk into the meeting with "the boss" with the two of you looking at the cucumber report. Ideally you want to say something like, "Last week we had 20 acceptance tests (aka gherkin scenarios) of 80 passing, 1 failing, and the rest unimplemented. Now week have 30 acceptance tests passing, 0 failing, and the rest unimplemented." Of course of accpetance test may be much for difficult and/ or time consuming to implement thatn another, and that does't really come thropugh too well in this report. However, this report tells you exactly what features were worked on in plain english language and whether it's working right now. If you're dealing with a more technical boss you can go into the actual methods of your code by going to your unit testing report such as this one or even your e2e reports like this one. If you have failing e2e tests that's kind of a bad thing so hopefully your e2e report is relatively boring. This is a great way to convey a ton of information; a complete snapshot of the project's development at any time. You can do this quickly and effectively and then talk about other things related to other coworkers, lunch, golf, etc. The boss can then refer back to these charts at any time after the meeting by visiting each corresponding url.

<div name="Sample Reports"></div>
### Sample Reports

Example of a cucumberjs acceptance tests report:

Cucumber reports are usually interactive an expandable. You can play with a [live demo here](http://htmlpreview.github.io/?https://github.com/gkushang/grunt-cucumberjs/blob/cucumber-reports/test/cucumber-reports/cucumber-report-bootstrap.html).

<img src="./images/cucumber-report-screenshot.png">


Example of a unit testing coverage report:
For Angular (and pretty much all front-end applications) code coverage is done with the *Istabul* library, and you only need focus on reading the report: 

<img src="./images/unit-test-report-directory-view.png">

<img src="./images/unit-test-report-file-view_js.png">


Example of an e2e report: I haven't found a nice open-source template to visualize this yet, but the e2e protractor script does output json reporting to a file:

```
[
  {
    "description": "should include jumbotron with correct data",
    "assertions": [
      {
        "passed": true
      }
    ],
    "duration": 1198
  },
  {
    "description": "should do nothing",
    "assertions": [
      {
        "passed": false,
        "errorMsg": "Expected 'some stuff' to equal 'oh,  whoops'.",
        "stackTrace": "Error: Expected 'some stuff' to equal 'oh,  whoops'.\n    at new jasmine.ExpectationResult (/Users/jameslynch/gits/ng-nj.org/node_modules/gulp-protractor/node_modules/protractor/node_modules/minijasminenode/lib/jasmine-1.3.1.js:137:32)\n    at [object Object].<anonymous> (/Users/jameslynch/gits/ng-nj.org/node_modules/gulp-protractor/node_modules/protractor/node_modules/minijasminenode/lib/jasmine-1.3.1.js:1349:29)\n    at [object Object].toEqual (/Users/jameslynch/gits/ng-nj.org/node_modules/gulp-protractor/node_modules/protractor/node_modules/jasminewd/index.js:248:11)\n    at [object Object].<anonymous> (/Users/jameslynch/gits/ng-nj.org/e2e/main.spec.js:22:26)\n    at /Users/jameslynch/gits/ng-nj.org/node_modules/gulp-protractor/node_modules/protractor/node_modules/jasminewd/index.js:94:14\n    at [object Object].promise.ControlFlow.runInFrame_ (/Users/jameslynch/gits/ng-nj.org/node_modules/gulp-protractor/node_modules/protractor/node_modules/selenium-webdriver/lib/goog/../webdriver/promise.js:1857:20)\n    at [object Object].promise.ControlFlow.runEventLoop_ (/Users/jameslynch/gits/ng-nj.org/node_modules/gulp-protractor/node_modules/protractor/node_modules/selenium-webdriver/lib/goog/../webdriver/promise.js:1729:8)\n    at [object Object].eval (/Users/jameslynch/gits/ng-nj.org/node_modules/gulp-protractor/node_modules/protractor/node_modules/selenium-webdriver/lib/goog/../webdriver/promise.js:2043:12)\n    at goog.async.run.processWorkQueue (/Users/jameslynch/gits/ng-nj.org/node_modules/gulp-protractor/node_modules/protractor/node_modules/selenium-webdriver/lib/goog/async/run.js:130:15)"
      }
    ],
    "duration": 1032
  }
]
```


---

<div name="Official Triplex Projects"></div>
## Part 6: Official Triplex Projects

Projects that are offically recognised as following Triplex methodologies.

<div name="NG-NJ"></div>
###NG-NJ

Github Repo: [https://github.com/ng-nj/ng-nj.org](#https://github.com/ng-nj/ng-nj.org)

Live Site: [https://ng-nj.github.io/ng-nj.org/](#https://ng-nj.github.io/ng-nj.org/)

This is the official home page for NG-NJ. This site began as a side project by Jim Lynch. It was built on AngularJS 1.4 and was scaffolded with the Gulp-Angular yeoman generator. This was the first project to be officially recognised as a Triplex Testing Project. 


<div name="Closing Thoughts"></div>
## Part 7: Closing Thoughts


<div name="The Mythical Fourth Plex"></div>
### The Mythical "Fourth Plex"
Triplex testing is based on the three core types of automated testing: acceptance tests, e2e tests, and unit tests. Armed with these, you're capable of incredibly solid coverage of your entire application. Often the unsual tests such as exploratory and smoke tests as grouped into the e2e testing category (as they should be). However, there are times when another method of automated testing emerges that doesn't fit into any of the three categories, and this is sometimes referred to as, "a fourth plex". For example,  [percy.io](https://percy.io/) is a tool for "visual regression testing" that can alert you of any unwanted visual changes from css or anything else. As new tools emerge and you find use cases for them in your work it would be silly not to take advantage of them. Just keep the core theories of Triplex testing in mind and view and fourth plex as an additional weapon in your automated testing arnesal.


<div name="Laid Back Perfectionism"></div>
### Laid Back Perfectionism
There is a type of culture that is instilled in teams that are working well in triplex testing development. Code is an interesting thing because if it isn't "perfect" it's not yet finished. I say *perfect* in quotes because the word can have many different meanings. Some may consider code with no errors and that contains no bugs when it runs to be perfect. For some, perfect code has a type of aesthetic requirement or must be in a certain style, and still others will say it's perfect if and only if all it's relevant tests from all three areas have been identified, written, and passing in all cases. "Laid back perfection" should be a mantra and part of the corporate culture. Obviously, humans are imperfect beings and at times make mistakes. The key is that there is a series of checks  and balances that prevents imperfect code from reaching the end of the pipeline, the users. The testing triplex acts as the team's ultimately safety net and acts as a safegaurd that only allows perfect code to be deployed. Thus, there is no need for developers to be in hyper-alert mode or to manually ensure that there are no bugs. Ideally, this results in perfect code being pushed live without headache or worry from the developer team.   

<div name="Why Test Your Own Code Is a Terrible Policy"></div>
### Why "Test Your Own Code" Is a Terrible Policy
Sadly, many companies simply don't take automated seriously enough.  If your company has a "test your own code policy" then it has a **superficial testing ideaology that is not truly a part of the development process** in the way that Triplex Testing prescribes. Acceptance tests in particular are not just the developer's responsibility but the responsiblity of *every* member of the team. Developers working with business analysts and other developers helps promote a better understanding of the codebase for everyone, fosters ubiquitous language, and allows the team to hammer down a collective understanding of the requirements (and have the in english writing that, as a bonus, is executable). As the company grows and junior developers are brought on "test your own code" becomes "test your own code... or not" and then the whole system really breaks down, and all of the sudden the team is not doing triplex testing at all! Harnessing these three automated testing methodologies can be challenging, and let's be honest- many great "production code" developers don't know the first thing about unit tests. Putting ownership on code files and assignments crushes colalboration and destroys opportunities for learning and intellectual advancement. Policy's like "test your own code" raise an even larger red flag about how the company attributes certain code to a particular person. This puts a lot of risk in *weak links*, depency on *tribal knowledge*, and it becomes diffult to pass of to a BAU team. Many agile circles agree that it is tremendously more beneficial for the developers and the end product itself if there is a *collective ownership* of the code.


<div name="Triplex Testing and the V-Model"></div>
### Triplex Testing and the V-Model
The V-Model is a common diagram used to describe the software lifecycle as phases and shows how the different levels of testing are importance at each phase. V-Model is a type of agile that highly values automated testing, specifically 4 types: acceptance testing, unit testing, system testing, and integration testing. Indeed, this may feel eerily similar to Triplex Testing which basically rolls up integration and system testing into one idea (although you could very well separate them into different configuration files if you wish). The V-Model diagram directly applies to Triplex Testing. The critical thing to remember about the V-Model is that it illustrates the business value at each stage of development of having all three (or four depending on how you look at it) suites of automated tests.


<div name="Effective Collaboration and Mob Programming"></div>
### Effective Collaboration and Mob Programming
Mob programming basically takes pair programming to the next level. A group of people site around one computer. One person is the navigater explaining what should be done next, one person is the driver typing at the keyboard, and everyone else helps as needed. Every so often you rotate. This concept is mentioned in an number of agile and BDD books since it is pretty much the ultimate form of communication and collaboration in the writing of all the code. There naturally becomes a very strong ubiquitous language, colelctive code ownership, and awareness of all relevant pieces. For more on Mob Programming check out this great podcast with Woody and the CucumberBDD team.6 They do a great job of defining *wasted time* and make an excellent business case for mob programming.

<div name="Exploratory Testing"></div>
### Exploratory Testing
Exploratorny testing is the act of testing the software with the intent of breaking it to uncover any potential bugs. Often times professional QA testers are great at this (even better than developers) because they bring a fresh perspective and have an intuition about where faults commonly occur in software.

Use a new protractor configuration file that is set up basically just like your e2e protractor file. This difference is in the type of protractor testst heat you will write here. 


<div name="Triplex Testing Community Groups"></div>
### Triplex Testing Community Groups
Please join our facebook group here(!!): [https://www.facebook.com/groups/triplextesting/](#https://www.facebook.com/groups/triplextesting/)


<div name="The Jasmine Vs. Chai Debate"></div>
### The Jasmine Vs. Chai Debate
It is unfortunate that we even have to have this "debate". Jasmine and Chai-Mocha are two different libraries for writing unit tests and doing assertions in tests. Jasmine seems to be more popular in the Angular community and it used by default for many scaffolded projects, karma, and protractor. I also personally like the syntax of Jasmine a little better, although both provide a BDD style "expect-to" syntax. The trouble with Jasmine is that is an "all-out unit testing framework" as opposed to a testing library and an assertion library. This means that you won't be able to use Jasmine-style assertions in your low level step definitions which is why we use Chai-Mocha in step definition tests.

<div name="The Importance of Having Conversations"></div>
### The Importance of Having Conversations
The process of developing software is a continuous journey of discovery. The concept of *The Three Amigos* is often used in BDD to represent the tester, the developer, and the business analyst. By having conversations and *really* thrashing out the details the team can get on the right path early and avoid unnecessary misunderstandings that often happen on projects with poor team communication. The result of these conversatins should be new or updates to existing examples written in the code as *scenarios*.


<div name="Triplex Tester Certification"></div>
### Triplex Tester Certification
If you've been practicing Triplex Testing Development for over a year and would like to take the official Triplex Tester Examination for the prestigious "Triplex Tester" designation then simply open an issue on this repo and a proctor will get in touch with you. 



---

<div name="FAQ"></div>
## Part 8: Frequently Asked Questions

<div name="Q1"></div>
### Q1. Is it wrong to treat low level step definitions like unit tests?
No. Although do you want to have coverage of all UI in web tests, going through the same GUI over and over to test the underlying business logic can slow down your test suite more than it needs to be. In the CucumberBDD Antipatterns podcast episode they describe having "all web tests" as an anti-pattern, and they recommend looking for opportunities to swap out web tests for faster-running unit test sytle step definitions.   

<div name="Q2"></div>
### Q2. Do I need to use acceptance tests?
**YES.** The acceptance tests are, arguably, the most important tests of all. These ensure that *you are building the right software.* Having feature files with scenarios written in Gherkin helps flesh out misunderstandings early, and provides developers with a clear path for *what to do next*, a classic issue for traditional TDD practictioners. You also miss out on the cucumber living documentation / generated reports and thus can't show it to the rest of the team. You requirements are written in some other palce (if at all) and quickly become out of sync with the code base. One simply cannot effectively do Triplex Testing without acceptance tests.  

<div name="Q3"></div>
### Q3. Do I need to use unit tests? 
**Yes.** The acceptance tests provide you with a way of checking that *you are building the right software*, but you still need to be sure that *you are building the software right.* Unit tests will pinpoint the exact line number of what's causing the problem where web tests will sometimes only be able to tell you *that something is broken, but not why.* Unit tests are key to having confidence in your code and encourages lots of worry-free refactoring. Write unit tests!  

<div name="Q4"></div>
### Q4. Do I need to use e2e tests?
**Yes.** The first time that Billy Bob's backend starts acting fishy and your program breaks, you're going to drive yourself crazy not knowing if it's an issue with your code or his code. If you are using **anything** external to your client side code, why not set up a tests solely to ensure that the endpoint works as expected?

<div name="Q5"></div>
### Q5. When should I NOT use the Testing Triplex?
Triplex Testing is a long-term way of developing serious projects that are meant to eventually go into production and have real users.  There is some set up and background knowledge required to correctly implement Triplex Testing. The only times you shouldn't use it are for throw-away test projects where you don't care about having buggy software, misunderstanding the stakeholders'requirements,or providing exactly the right functionality. 

<div name="Q6"></div>
### Q6. Most Cucumber / BDD examples have a root level "features" folder. Why don't you follow this convention?
Having a root level features folder with a complete parrallel directory structure is an old-school pattern from before we had nice built scripts that could pull out test files from the src directory. The key thing to avoid is **scrolling like mad syndrome**, a problem that occurs when you have parralel directory structures. Symptoms of this virus are developers cursing themselves and their projects because their are forced to violently scross through their project explorer to find companion files for some simple comnponent. Don't give your projects *scrolling like mad syndrome.* Don't create parrallel directories of your whole project. 

<div name="Q7"></div>
### Q7. My boss says we don't have enough time for testing. What should I do?
Remind him that nobody wants 99% code. Every project should be given the earnest effort that it deserves, and nothing should be done half-heartedly. If there isn't enoguh time for perfect code, the project shouldn't begin in the first place. 

<div name="Q8"></div>
### Q8. Can't we just manually test everything?
Manually testing is easy for incredibly small projects, but as the codebase grows manual testing quickly becomes time-consuming, expensive, error-prone, and just plan infeasible. You can't take advantage of all the browsers on Sauce Labs, and you get any automatically generated reports from manual testing. Manual testing should only really be used as a last resort and a means for exposing useful exploratory tests (that could then be automated once found).

<div name="Q9"></div>
### Q9. Will the theory of Triplex Testing work for [insert favorite platform here]?
Yes! Although in this guidebook I focused on JavaScript and AngularJS, the theory of combining acceptance, unit, and e2e tests can be applied to virtually any front-end platform, and even backend software as well! 

Works Cited 
1. Test Pyramid Article by Martin Fowler: [http://martinfowler.com/bliki/TestPyramid.html](#http://martinfowler.com/bliki/TestPyramid.html)
2. [CucumberBDD Podcast - Cucumber Anti-Patterns](#https://cucumber.io/blog/2016/05/09/cucumber-antipatterns)


3. reporting

4. [Agile Manifesto](#http://agilemanifesto.org/)
5. [Living Documentation Article](#http://searchsoftwarequality.techtarget.com/definition/living-documentation)
6. [Mob Programming CucumberBDD Podcast Episode](#https://cucumber.io/blog/2016/04/19/mob-programming)

---

This guide is maintained by ng-nj, the Angular Group of New Jersey.

## Disclaimer
THIS GUIDE IS PROVIDED "AS IS" AND ANY EXPRESSED OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE REGENTS OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION)
HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
