# DOM Testing Library

- the core library, `DOM Testing Library`, is a light-weight solution for testing web pages by querying and interacting with DOM nodes (whether simulated with JSDOM/Jest or in the browser)

  - main utilities it provides involve querying the DOM for nodes in a way that's similar to how the user finds elements on the page. In this way, the library helps ensure our tests give us confidence that our application will work when a real user uses it

- There is also a plugin to use testing-library queries for end-to-end tests in `Cypress`

## What this library is not

1. a test runner of a framework
2. specific to a testing framework

- `DOM Testing Library` works with any environment that provides DOM APIs, such as _Jest, Mocha + JSDOM_, or a real browser

## What you should avoid with Testing Library

### Avoid testing implementation details

- there are two distinct and important reasons to avoid testing implementation details. Tests which test implementation details

  - can break when we refactor code application -> **false negatives**
  - may not fail when we break application code -> **false positives**

- **implementation details are things which users of your code will not typically use, see, or even know about**

- _to be clear, the test is: "does the software work". If the test passes, then that means the test came back "positive" (found working software). If it does not, that means the test comes back "negative" (did not find working software). The term "False" refers to when the test came back with an incorrect result, meaning the software is actually broken but the test passes (false positive) or the software is actually working but the test fails (false negative)_

#### False negatives when refactoring

- tests which test implementation details can give us a false negative when we refactor our code. This leads to brittle and frustrating tests that seem to break anytime we so much _"as look at the code"_.

#### False positive test

- it means that we didn't get a test failure, but we should have!

### Implementation detail free testing

- **Our test should typically only see/interact with the props that are passed, and the rendered output**
- free from these implementing details:
  - internal state of component
  - internal methods of the component
  - lifecycle methods of the component
  - child components

### The guiding principles

- emphasizes to focus on tests that closely resemble how your web pages are interacted by the users

  - **the more our tests resemble the way our software is used, the more confidence they can give us**

- utilities are included in this library based on the following guiding principles:
  - if it relates to rendering components, then it should deal with DOM nodes rather than component instances, and it should not encourage dealing with component instances.
  - it should be generally useful for testing the application components in the way the user would use it
  - utility implementations and APIs should be simple and flexible

## React-Testing-Library (RTL)

- builds on top of `DOM Testing Library` by adding APIs for working with React components
