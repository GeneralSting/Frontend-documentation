# Rules of React

- just as different programming languages have their own ways of expressing concepts, React has its own idioms — or rules — for how to express patterns in a way that is easy to understand and yields high-quality applications
  - writing idiomatic React code can help you write well organized, safe, and composable applications. These properties make your app more resilient to changes and makes it easier to work with other developers, libraries, and tools
  - `Strict Mode`
  - **ESLint plugin**

## Components and hooks must be pure

- purity in components and hooks is a key rule of React that makes your app predictable, easy to debug, and allows React to automatically optimize your code

## React calls components and hooks

- React is responsible for rendering components and hooks when necessary to optimize the user experience
  - it is declarative: we tell React what to render in your component’s logic, and React will figure out how best to display it

## Rules of hooks

- hooks are defined using JavaScript functions, but they represent a special type of reusable UI logic with restrictions on where they can be called
