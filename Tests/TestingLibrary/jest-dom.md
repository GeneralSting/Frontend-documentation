# jest-dom

- companion library for `Testing Library` that provides custom DOM element matchers for `Jest`

## The problem

- wa want to use `jest` to write tests that assert various things about the state of a DOM. As part of that goal, wa want to avoid all the repetitive patterns that arise in doing so. Checking for an element's attributes, its text content, its css classes...

## The solution

- the `@testing-library/jest-dom` library provides a set of custom jest matchers that we can use to extend jest. These will make ours tests more declarative, clear to read and to maintain
