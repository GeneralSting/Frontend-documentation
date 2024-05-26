# Package Management

## npm arhitecture

1. npm client/Yarn...
2. npm repository

- consists of two main parts
  - npm client or any other alternative requests access to the third party libraries stored in cloud base npm repository

## Module vs package

- module is a single JS file that contains code
- package contains one or more JS or any other language code files and `Package.json` file which groups all files

## Node modules and package lock

- `package.json`

  - used for more then dependencies - defining project properties, description, author, license information...
  - records the minimum version app needs, if app gets update for versions of a particular package, the change is not going to be reflected in this file

- `package-lock.json`
  - used to lock dependencies to a specific version number
  - records the exact version of each installed package which, future installs will be able to build an identical dependency tree

| Node_modules                     | Package-lock.json            |
| -------------------------------- | ---------------------------- |
| do not manually modify           | do not manually modify       |
| do not check into source control | do check into source control |
