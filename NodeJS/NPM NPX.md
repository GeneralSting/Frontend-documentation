# NPM vs NPX

## NPM

- node package manager
- manages packages but doesn't execute any
- npm by itself does not simply run any package
  - it does not run any package as a matter of fact
  - if you want to run a package using NPM, package must be sepcified in `package.json` file
- when executables are installed via npm packages, npm links to them:

  1. local installs have `links` created at `./node_modules/.bin` directory
  2. global installs have `links` created from the global `bin/` direcotry (e.g. /usr/local/bin)

- only globally installed packages can be executed by typing their name only
  - to fix this and have it run, local path must be typed (./node_modules/.bin/some-package)
- run locally installed package (project package) by editing `package.json` file and adding that package in the `scripts` section
  - npm run some-package

## NPX

- node package executor
- the package runner
- npx checks whether command exitsts in certain patch or in the local project binaries and execute it.
- npx some-package
- has ability to execute a package which wasn't prevously installed

  - npx create-react-app my-app
    - generates a react app boilerplate within the path the command had run in, and ensures that you always use the latest version of a generator or build tool without having to upgrade each time

- npx command may be helpful in the script section of a package.json file, when it is unwanted to define a dependency which might not be commonly used or any other reason:

```js
"scripts": {
    "start": "npx gulp@3.9.1",
    "serve": "npx http-server"
}
```

- Call with: npm run serve
