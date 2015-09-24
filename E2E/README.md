# Protractor
> Best practices using Protractor


The tool for e2e testing your AngularJS application is [Protractor](https://angular.github.io/protractor/#/). Protractor is an e2e test framework built on top of WebDriverJS, which adds some Angular-specific functionality.

End to end(e2e) tests cover the interaction scenarios between the end user and your application. This works by having the test code simulate a series of user actions against certain UI parts of your application and then making some assertions regarding what the expected result of those actions should be.

So let's pretend we have a simple application that can answer any question. Let's call it the "Jedi Master of All Knowledge" app. The idea of the app is: the user enters a question in an input field, presses a button and gets the answer to the question.

The HTML for the application would look like:

```html
<!-- jedimaster.html -->

  <body ng-app="JediMasteroffAllKnowlegde">
    <div class="question">
      <input class="question__field" ng-model="question.text"
             placeholder="What would you like to ask Jedi Master od All Knowledge?">
      <button class="question__button" ng-click="answerQuestion()"
              ng-disabled="!question.text">?</button>
    </div>
    <div class="answer">{{answer}}</div>
  </body>
  ```
  
The e2e spec  should cover exactly the interaction we described earlier: user enters question, presses button and gets an answer. They would look just like this:

```javascript
/* jediMasterSpec.js */

  describe("Jedi Master of all knowledge module", function() {

      var question = element(by.model('question.text'));
      var answer = element(by.binding('answer'));
      var button = element(by.className('question__button'));

      beforeEach(function() {
          browser.get('/#/jedi-master-of-all-knowledge');
      });

      it('jedi master should answer any question', function() {
          question.sendKeys("What is the purpose of life?");
          button.click();
          expect(answer.getText()).toEqual("Code!");
      });

      it('jedi master should not answer empty questions', function() {
          question.sendKeys("    ");
          expect(button.isEnabled()).toBeFalsy();
      });
  });
```