### Protractor

http://angular.github.io/protractor/#/

> Ptotractor is an e2e test framework for AngularJS applications. Protractor is a Node.js program built on top of WebDriverJS. Protractor runs tests against your application running in a real browser, interacting with it as a user would

### Karma

https://github.com/karma-runner/karma

> Spectacular Test Runner for Javascript

When should I use Karma?

- to test code in **real browser**
- to test code in *multiple browsers* (desktop, mobile, tablets)
- to execute your tests locally during development
- to execute your tests on a CI server
- to execute your tests on every save

### Karma vs Protractor

- use **Karma** for unit testing
- use **Protactor** for e2e or intergration testing

> Karma is a great tool for unit testing, and Protractor is intended for end to end or integration testing. This means that small tests for the logic of your individual controllers, directives, and services should be run using Karma. Big tests in which you have a running instance of your entire application should be run using Protractor. Protractor is intended to run tests from a user's point of view - if your test could be written down as instructions for a human interacting with your application, it should be an end to end test written with Protractor.

### Advanced Testing and Debugging in AngularJS

http://www.yearofmoo.com/2013/09/advanced-testing-and-debugging-in-angularjs.html

### Jasmine vs Mocha + Chai + Sinon

http://thejsguy.com/2015/01/12/jasmine-vs-mocha-chai-and-sinon.html

Mocha is a testing framework
Chai is a assertion library
Sinon is a mocking library

Jasmine is all in one
