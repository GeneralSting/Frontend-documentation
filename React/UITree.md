# UI as a tree

- browsers use tree structure to model HTML (DOM) and CSS (CSSOM - CSS Object Model, set of APIs allowing the manipulation of CSS from JS)
- mobile platforms also use trees to represent their view hierarchy
- React creates a UI tree from components - UI tree is used to render to the DOM

![React UI tree](https://react.dev/_next/image?url=%2Fimages%2Fdocs%2Fdiagrams%2Fpreserving_state_dom_tree.dark.png&w=1920&q=75)

- React also uses tree structure to manage and model the relationship between components

## The Render Tree

- the tree is composed of nodes, each of which represents a component
- the root node in React render tree is the `root component` of the app
- top-level components are the components nearest the root component and affect the rendering performance of all the components beneath them and often contain the most complexity
  - leaf components are near the bottom and have no child components, often frequently re-rendered

## The module dependency tree

- another relationship in React app - app's module dependencies
- each node in a module dependecy tree is a module and each branch represents `import` statement in that module
- the root node of the tree is the root module, also known as the entrypoint file

- building app for production - bundler will use the dependency tree to determine what modules should be included
