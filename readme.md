# Testing with Jasmine

## Screencasts

- [Part 1/3](https://youtu.be/sT-YhpEIMPQ)
- [Part 2/3](https://youtu.be/3J3W0Hi2Jxw)
- [Part 3/3](https://youtu.be/GMafQUii6Qc)

## Learning Objectives

* List benefits of unit testing in collaborative development process.
* Identify language-agnostic patterns in testing syntax and methodology.
* Differentiate the roles of and relationships between `suite`, `spec`, and `expectation` in the context of Jasmine testing.
* Implement `beforeEach()` and `afterEach()` to DRY up test code.
* Use the `jasmine-node` CLI to run Jasmine tests.
* Plan a project by creating a series of unit tests that define its parameters.

# Do You Even Test, Bro?

### Why do we implement tests in our applications? (5 min)

As our applications increase in complexity, we need a safety net.  We need something to ensure that we "Do no harm".  We need a battery of automated tests.  These are specifications about YOUR code that you can run to ensure your code is doing what it should.  

Think back to the way you code.  You create a part of a web page, then you browse to that page to test it.  To ensure that it is doing as you expect.  Then you add another feature.  And test both features.  Then you add a third feature and test... just the third feature.  Imagine if you had a battery of automated specs, which run against your code, so you can see if your new changes fit your new requirements and EVERY requirement that came before this.

### Unit testing (5 min)

**Unit tests** check the smallest level. The functionality of a specific method.

  * The "units" in unit tests are individual methods. Unit tests are intended to test small, little blocks of code, and make sure a specific input results in a specific output.

  * As a rule of thumb, a good unit test should not be more than 5 lines long.

**Employers give you major bonus points for it!**

You'll see the term **test coverage** pop up pretty often. People are always aiming for "100% test coverage". If your app has 100% test coverage, that means every single method in your app has a unit test verifying that it works.

>For instance, while it's easy and free to write Salesforce apps, Salesforce will only add your app to its "app store" if you've obtained 100% test coverage, and Salesforce's developer team can run your tests and have them all pass.

**What are the reasons testing is so important? Why would employers love it so much?**

<!-- Real World Example: DC Tech Startups -->
<!--5 people from wdi7 cohort hired by Accella in charge of creating rspec tests  -->
<!--Planning on talking about two startups interviewed with and how wished they would have integrated more testing earlier on when developing their applications, it's now a big focus for them, cut corners early on and now need to refactor code base -->

We've asked you to write user stories. Writing unit tests is a very similar process.

When we think of "testing" we tend to think of something you do *after* you've created something. With unit tests, you're encouraged to write the tests *first* before you even start writing actual code.

### Turn and talk (5 min)

Turn to a partner and discuss reasons of why would you write tests beforehand?

>Answers

>When you write tests first, you're creating a tidy little checklist for yourself of things to complete. The **goal of unit tests** is that **when all of the tests pass, your app is complete**.

>You're used to thinking the other way around: when the app is complete, all the tests should pass. Writing the tests first forces you to think about what an app really *needs* to do to be complete. It forces you to scope things down to your MVP. It forces you to think of your app as a bunch of little pieces, rather than one big behoemeth.

>In short: writing out unit tests, even if you just leave them pending, will make this class much easier, and make you look super-marketable.

>This process of writing the tests **first** is called **Test-Driven Development**, or TDD.

### TDD Overview: (5 min)

Why isn't testing more common?

* Cons
  * **Time.** It's a waste of my time and effort to test.
  * **It's too much.** I can test just fine using the console.
  * **App complexity.** My app is too simple to require testing.

Why bother testing?

* Pros
  * **Bug detection.** Quickly identify unanticipated errors.
  * **Code Quality.** Create standards for our code before writing it.
  * **Time.** Shorten development time through bug detection.
  * **Documentation.** Tests act as a documentation of sorts for how our code should work. Helpful to other developers and shareholders.
  * **Jobs.** Testing is a job requirement across the board.

### Do you wanna build a snowman?

For example, imagine you're Elsa from Frozen, creating a simple program/app that
will build a snowman.

Before we write any of our snowman code, we're going to create a test. And
before we create a test, we're going to think: What do I want my snowman builder
to do? What should the snowmen it creates be like?

```js
//I want my snowman builder to create a snowman object
//My winter wonderland is a friendly place, so I want each snowman to have a name
//In order for it to really be a snowman, it needs to have a carrot nose.
//It also needs stick arms.
//If the snowman is named Olaf, he should like warm hugs.
```

Now that we have an English-y outline, we're going to start turning it into tests.

### Jasmine?

Today we'll be using a Javascript testing framework called Jasmine. It's the
same thing as RSpec, just for Javascript. It uses "describe" and "it", just like
RSpec. Jasmine, uses `describe` and `it` methods to express whats going on in
the code more like a conversation.

Tests follow a "describe...it" format, like so:

- describe "A snowman"
  - it "should have a name"
  - it "should have a carrot nose"
  - it "should have stick arms"
  - describe "a snowman named Olaf"
    - it "should like warm hugs"

Jasmine is only one of many testing framework. There's [Mocha](https://mochajs.org/), [QUnit](https://qunitjs.com/) and more... However, they're all very similar. Most use the same "describe...it" syntax.

- [RSpec vs. Jasmine Syntax](https://gist.github.com/kevinbuch/6611072)

#### Getting set up (5/55)

First, we're going to install jasmine-node globally.

It doesn't matter where you run this code:

```bash
$ npm install  -g jasmine-node
```

Now, `cd` into your project folder. If you don't have a project folder, go ahead and make one. It doesn't really matter what folder you use for what we're about to do, but if you can, you may as well get some of your project done now so you don't have to later!

I'm going to create a folder for a `snowman-builder` project.

Inside your project folder, create a new folder called `spec`:

```bash
$ mkdir spec
```

Inside that new folder, create a file named after your model, followed by "dash-spec":

```bash
$ touch spec/snowman-spec.js
```

Now, run:

```bash
$ jasmine-node spec
```

You should get something like:

```
$ jasmine-node spec


Finished in 0.001 seconds
0 tests, 0 assertions, 0 failures, 0 skipped
```

## I do: Javascripting your tests (10/65)

Now, I'll paste the psuedocode we wrote earlier into the `-spec.js` file we created.

If I run `jasmine-node` at this point, I'll just get an error. We need to
properly format the code for Javascript.

A Jasmine test file will look like this:

```js
describe("the test subject", function(){

  it("should have this quality", function(){

  });

  it("should have this other quality", function(){

  });

});
```

`describe` and `it` are actually functions, just like, say, `console.log()`. They both take a string as their first argument. The second argument is a callback function.

A `describe` statement's function contains a bunch of `it` statements.

An `it` statement's function contains the code that will do the actual testing. We're not going to write that code yet -- we're just going to worry about getting set up with the proper syntax.

For the snowman builder, the result would be this:

```js
describe( "A snowman", function(){

  //My winter wonderland is a friendly place, so I want each snowman to have a name.
  it( "should have a name", function(){

  });

  //In order for it to really be a snowman, it needs to have a carrot nose.
  it("should have a carrot nose", function () {

  });

  //It also needs stick arms.
  it("should have stick arms", function () {

  });

  //If the snowman is named Olaf, he should like warm hugs.
  describe( "a snowman named Olaf", function(){

    it( "should like warm hugs", function(){

    });

  });

});
```

If I run this, I now get:

```
$ jasmine-node spec
....

Finished in 0.009 seconds
4 tests, 0 assertions, 0 failures, 0 skipped
```

Just like in RSpec, each green dot indicates a passing test.

If I add the `--verbose` flag, I get:

```
$ jasmine-node spec --verbose

A snowman - 4 ms
    should have a name - 1 ms
    should have a carrot nose - 0 ms
    should have stick arms - 0 ms

    a snowman named Olaf - 0 ms
        should like warm hugs - 0 ms

Finished in 0.01 seconds
4 tests, 0 assertions, 0 failures, 0 skipped
```

## You Do: Update your code so that it has the proper syntax (15/80)

This includes adding the appropriate parentheses, double-quotes, semicolons, and functions.

When you're done, you should be able to run `jasmine-node spec` with no failing tests.

The fact that these tests "pass" doesn't really mean anything since the tests don't actually test anything -- but at least we know there aren't any syntax errors.

# The suite life of Jasmine (5/85)

Let's break this test down according to its parts.

What you've done so far is create a **test suite**.

1. **The Suite**.

```js
describe( "A snowman", function(){
  // Specs go here.
});
```

A "suite" is the highest-level container in our test file.
* A suite defines what we are testing. Oftentimes, this is an object.
* Indicated using the `describe` function.
* Takes two arguments: (1) a string, (2) a function
  * (1) The string is the name of what we are testing
  * (2) The function contains the actual tests

**2. The Specs**

A suite contains **specs**. These are the `it` statements.

In the "spec," we target a specific part of the suite.

> "Spec" is short for "specification", which comes from "specific", as in, "we're testing a specific part of this app." Get it?

[Docs on what we've covered](http://jasmine.github.io/1.3/introduction.html) up until **Expectations**

## Break (10/95)

# Great Expectations! (10/105)

Now that we have the pieces of our snowman builder described, we can start thinking about how we'll know that our snowmen are living up to our expectations.

**Expectations** are the meat-and-potatoes of our tests.
* Begins with code content. In this case, saves the name of the person in question to a variable.
* Last line is the actual expectation.
  * Begins with `expect`. Takes one argument, the variable whose value we are testing.
  * Followed by a **matcher** (e.g., `toBe`), which tests the expectation in a particular way.

### Jasmine's built-in matchers

```txt
'toBe' matcher compares with ===
'toEqual' matcher
'toMatch' matcher is for regular expressions
'toBeDefined' matcher compares against `undefined`
'toBeUndefined' matcher compares against `undefined`
'toBeNull' matcher compares against null
'toBeTruthy' matcher is for boolean casting testing
'toBeFalsy' matcher is for boolean casting testing
'toContain' matcher is for finding an item in an Array
'toBeLessThan' matcher is for mathematical comparisons
'toBeGreaterThan' matcher is for mathematical comparisons
'toBeCloseTo' matcher is for precision math comparison
'toThrow' matcher is for testing if a function throws an exception
'toThrowError' matcher is for testing a specific thrown exception
```

One thing to note is that there isn't a built-in matcher for checking whether something is a specific type of object. There's no, `expect( olaf ).toBeA(Snowman)` (for who-knows-what reason).

To test whether something is an object of a specific type, there are several things you could try:

```txt
expect( olaf.name ).toEqual(jasmine.any(String));
expect( typeof olaf.name ).toBe("string");

expect( olaf.constructor.name ).toBe("Snowman");
expect( olaf instanceof Snowman).toBeTruthy();
```

Those last two won't work with function expressions (`var Snowman = function(){}`); only with function declarations (`function Snowman(){}`).

A full list of Jasmine's native matchers can be found [here](http://jasmine.github.io/edge/introduction.html#section-Expectations).

If you're feeling adventurous, you can even [create your own custom matcher](http://jasmine.github.io/2.0/custom_matcher.html).

## Let's add the first expectation:

```js
describe( "A snowman", function(){

  //My winter wonderland is a friendly place, so I want each snowman to have a name.
  it( "should have a name", function(){
    var olaf = new Snowman("Olaf");
    expect( olaf.name ).toBeDefined();
  })

  // ... more stuff
});
```

It fails!

```txt
$ jasmine-node spec
F...

Failures:

  1) A snowman should have a name
   Message:
     ReferenceError: Snowman is not defined
   Stacktrace:
     ReferenceError: Snowman is not defined
    at null.<anonymous> (/Users/robertthomas/Desktop/foo/spec/s-spec.js:5:20)

Finished in 0.012 seconds
4 tests, 1 assertion, 1 failure, 0 skipped
```

That's because this script has no idea what a Snowman is -- we haven't linked in a file that describes a Snowman model yet.

So I am going to create a `snowman.js` file and put this in it:

```js
// /snowman.js

function Snowman(name) {
  this.name = name;
  this.features = ["carrot nose", "stick arms"];
}

module.exports = Snowman;
```

Next, I am going to `require` that file inside my spec file:

```js
var Snowman = require("../snowman");

describe( "A snowman", function(){

  //My winter wonderland is a friendly place, so I want each snowman to have a name.
  it( "should have a name", function(){
    var olaf = new Snowman("Olaf");
    expect( olaf.name ).toBeDefined();
  });

  // ... more stuff
});
```

...and now the test passes!

# The Process, Recontextualized (5/110)

### Test-driven development

![tdd flowchart](img/tdd.png)

A planning-oriented approach TDD
  - **Think.**
    - What do we want this app/feature to do?
    - What are its components? (Think models!)
    - What properties should each of those components have? What should they be able to do?
    - What behaviors do you definitely want to avoid?
  - **Write _tests_ an outline of your app/feature using testing syntax.**
    - For today, we are going to break this down even further, first writing suites and specs, then going back and adding expectations.
  - **Run your tests.** Seeing red.
  - **Write code.** How can we make this test pass?
  - **Test passes.** Green light.
  - **Refactor and Repeat.**

You write a failing test. Your next step is to write code that will make your test pass. This is kind of like Jeopardy, where the contestants are given the answer and then come up with a question for that answer: it is backwards from what we intuitively want to do, which is write passing code first and test it later.

This process is often abbreviated **Red, Green, Refactor**: write a failing test, write the code to make it pass, then refactor. Lather, rinse repeat.

### TDD vs. BDD

- TDD is mainly a process to help developers create a well-written unit of code that does a set of tasks. And to allow developers to be confident in their code.
> TDD ensures that you built the software correctly, not that the correct software was built.

- BDD combines the TDD process with ideas from DDD (domain-driven design). The biggest difference is that the syntax reads more like english and could be shared with non-programmers as specification for what the code should do.
>BDD codifies customer requirements into discrete, real-life scenarios.

  - Jasmine is a behavior driven framework

Check out these great articles comparing TDD & BDD:
- [Unit Testing TDD & BDD](http://codeutopia.net/blog/2015/03/01/unit-testing-tdd-and-bdd/)
- [TDD vs. BDD](http://joshldavis.com/2013/05/27/difference-between-tdd-and-bdd/)
- [TDD & BDD](http://www.joecolantonio.com/2014/07/29/unit-tdd-and-bdd-testing-whats-the-difference/)

### All Together Now (10/20)

When it comes to development in teams, both the benefits and the potential pitfalls of testing practices increase. Many feel that testing is essential when working on large, complex projects.

* Take Ember.js for example. [If you look at the framework's repo](https://github.com/emberjs/ember.js#how-to-run-unit-tests), it comes packaged with a ton of tests.
* So many moving parts. And so many people contributing to them. Can you imagine how crazy this would get without testing?

Testing is another thing that's a little hard to appreciate through this class
because we mostly work alone to make relatively small apps. Working together on
this project, you're likely to find that you lose whole hours manually testing
your app: quitting Node, re-seeding your database, starting Node, opening your
app in the browser, clicking through each page. Testing eliminates this for you,
and makes for a much less stressful week.

Two common pain points in the wild are creating test coverage for existing code
bases and ensuring that test suites are adequately maintained as an application
grows in complexity. BOTH of these can be avoided by using TDD as a tool for
***planning***.  

# In the "real world"... (10/120)

...at this point we would write one more expectation, then write the code to
make it pass, then write the next expectation, and so on, doing everything **one
test at a time**.

However, we're limited by time in this class, so I'm going to show you what the
end result for this Snowman would look like, and then ask you to write all your
own expectations.

Q. Why is it not recommended to write *all* your expectations first, and then write all the code to make them pass?
---
> Because it's pretty straightforward to write the code to make one failing test into a passing test. It's super-overwhelming to write the code to make a bunch of failing tests pass.

## The final Snowman specs:

```js
var Snowman = require("../snowman");

describe( "A snowman", function(){

  //My winter wonderland is a friendly place, so I want each snowman to have a name.
  it( "should have a name", function(){
    var olaf = new Snowman("Olaf");
    expect( olaf.name ).toBeDefined();
  });

  //In order for it to really be a snowman, it needs to have a carrot nose.
  it("should have a carrot nose", function () {
    var olaf = new Snowman("Olaf");
    expect ( olaf.features ).toContain("carrot nose");
  });

  //It also needs stick arms.
  it("should have stick arms", function () {
    var olaf = new Snowman("Olaf");
    expect ( olaf.features ).toContain("stick arms");
  });

  //If the snowman is named Olaf, he should like warm hugs.
  describe("A snowman named Olaf", function(){
    it( "should like warm hugs", function(){
      var frosty = new Snowman("Frosty");
      var olaf = new Snowman("Olaf");
      expect( olaf.hug() ).toBe( "I like warm hugs!" );
      expect( frosty.hug() ).not.toBe( "I like warm hugs!" );
    });
  });

});
```

I'm not even going to bother running `spec` because I know all but one of these tests will fail. That's not important right now. The important thing is that I am writing `expect` statements that make sense to me because this will inform the coding decisions I make later.

## You do: Add expectations to your code (20/140)

You have two goals:
- To write expectations that make sense in English...
- ...while still being valid Javascript: you close all your parentheses, put semicolons where you need them, and so on.

Consider: What variables do you need to test? From an English perspective, what names would it make sense for the different variables and methods to have?

## Refactor (10/150)

Q. What is not DRY about my tests? What repeats?
---
> `var olaf = new Snowman("Olaf");`

In RSpec we could DRY up tests by making a piece of code run before each test. We can do the same thing here:

``` js
describe( "A snowman", function(){
  var olaf;

  beforeEach(function(){
    olaf = new Snowman("Olaf");
  });

  it( "should have a name", function(){
    expect( olaf.name ).toBeDefined();
  });

  it("should have a carrot nose and stick arms", function () {
    expect ( olaf.features ).toContain("carrot nose", "stick arms");
  });

  describe("A snowman named Olaf", function(){
    var frosty;
    it( "should like warm hugs", function(){
      frosty = new Snowman("Frosty");
      expect( olaf.hug() ).toBe( "I like warm hugs!" );
      expect( frosty.hug() ).not.toBe( "I like warm hugs!" );
    });
  });

});
```

### Let's Test It Out!
That looks like a good test to me. Let's run it!
* From your in-class folder, run: `$ jasmine-node spec`
* What error do we get?

Of course, the rest of the tests are still "failing". The fact that they are running shows that my syntax is good to go, but I need to write the rest of the code to be tested.

### Let us Build a Snowman!

```js
// /snowman.js
function Snowman(name) {
  this.name = name;
  this.features = ["carrot nose", "stick arms"];
}

Snowman.prototype = {
  hug: function(){
    if (this.name == "Olaf") {
      return "I like warm hugs!";
    }
    else {
      return "Why are you hugging snow?";
    }
  }
};

module.exports = Snowman;
```

Let us run our test again: `$ jasmine-node spec`

```
$ jasmine-node spec --verbose

A snowman - 7 ms
    should have a name - 4 ms
    should have a carrot nose - 1 ms
    should have stick arms - 0 ms

    A snowman named Olaf - 1 ms
        should like warm hugs - 1 ms

Finished in 0.014 seconds
4 tests, 5 assertions, 0 failures, 0 skipped
```

## Asynchronous tests

One last thing to note is that while you can test AJAX requests and database interactions, it's a little tricky because they're asynchronous. **Make sure you use .then()**.

Here are some examples:

```js
// ...
it("can be saved to the database", function(){
  var olaf = new Snowman("Olaf");
  olaf.save().then(function(err, docs){
    // err will always be null if the database action was successful
    expect( err ).toBeNull();
  });
});

it("makes a successful AJAX request", function(){
  var olaf = new Snowman("Olaf");
  $.getJSON("http://snowhub.com").then(function(response){
    expect( response[0].name ).toBe( "John Snow" );
  });
});
```

## And that's a wrap

The snowman code is available here:

https://github.com/ga-dc/snowman_building_with_jasmine

# Testing Terminology

### Test Types: Unit vs. Integration vs. End-to-End

> “If you wish to converse with me –define your terms” ~Voltaire

- **Unit Tests**
Unit tests isolate the smallest piece of a feature, typically a method/function in isolation. In short, unit tests are as simple as possible, easy to debug, reliable (due to reduced external factors), fast to execute and help to prove that the smallest building blocks of your program function as intended before they're put together. The caveat is that, although you can prove they work perfectly in isolation, the units of code may blow up when combined.

- **Integration Tests**
An integration test takes a small group of units, often two units, and tests their behavior as a whole, verifying that they coherently work together. Sometimes you need to have tests to verify that two separate systems – like a database and your app – work together correctly, and that calls for an integration test. As a result, when validating integration test results, you could for example validate a database related test by querying the database to check the database state is correct.

- **End-to-end/Acceptance/Functional Tests**
Involve performing tests on the full system (e.g. using your web page via a web browser) to see whether the application's functionality satisfies the specification. E.g. "clicking a zoom icon should enlarge the document view by 25%." There is no real continuum of results, just a pass or fail outcome.
_**Note** All three generally mean the same thing but not always_

![testing pyramid](img/testing-pyramid.png)

> As a good first guess, Google often suggests a 70/20/10 split: 70% unit tests, 20% integration tests, and 10% end-to-end tests. The exact mix will be different for each team, but in general, it should retain that pyramid shape.

## Quiz Questions
- Put the following actions in order, from what should happen first to what should happen last:
  1. Write the code for your app
  - Write an English-y outline of your app's models and what they should do
  - Write passing tests for your app
  - Refactor your app's code
  - Write failing tests for your app

  > Outline, failing (red), write code, passing (green), refactor

- What's the difference between a `suite`, a `spec`, and an `expectation`?
  > A suite is a series of tests that describe a particular object or feature; a spec is one test; an expectation is the code that goes inside the spec that does the actual testing

- What's the difference between `describe`, `it`, and `expect` statements?
  > `describe` is a suite; `it` is a spec; `expect` goes inside a spec

- What does `beforeEach` do?
  > Contains code that is run before each spec

## Exit Ticket (3 min)

Before you leave, plase take ~3 minutes to complete [this exit ticket.](https://docs.google.com/forms/d/1d03NYFphG6m7yAMUY1OlnJZMQWof7Rt6b5MX3Xn4ZPs/viewform)

This helps us help you! We'll review responses for each exit ticket and start to implement them in future lessons.

## Additional Reading

* [Jasmine's really great documentation](http://jasmine.github.io/2.1/introduction.html)
* [RSpec vs. Jasmine Syntax](https://gist.github.com/kevinbuch/6611072)
* [Creating Custom Matchers in Jasmine](http://jasmine.github.io/2.0/custom_matcher.html)
* [Testing AJAX Calls with Jasmine](http://jasmine.github.io/2.1/ajax.html)
* [Unit Testing TDD & BDD](http://codeutopia.net/blog/2015/03/01/unit-testing-tdd-and-bdd/)
* [TDD vs. BDD](http://joshldavis.com/2013/05/27/difference-between-tdd-and-bdd/)
* [TDD & BDD](http://www.joecolantonio.com/2014/07/29/unit-tdd-and-bdd-testing-whats-the-difference/)
* [Say no to more E2E testing](http://googletesting.blogspot.com/2015/04/just-say-no-to-more-end-to-end-tests.html)
* [Unit vs. functional vs acceptance vs integration](http://stackoverflow.com/questions/4904096/whats-the-difference-between-unit-functional-acceptance-and-integration-test#answer-4904533)
