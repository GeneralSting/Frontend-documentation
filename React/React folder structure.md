## Folder structure for large scaling projects

### project name
- node_modules
- public
- #### src
    - ##### assets
        1. downloaded css, image and all other files that are not js file
    - ##### components
        - <b>ui</b>
        - <b>form</b>
        - ...
        1. components that are shared accros app, shared components
    - ##### context
        1. all context files
    - ##### data
        - <b>configValues.js<b>
        1. js files, const values
    - ##### features
        - <b>authentication</b>
            - <b>components</b>
            - <b>hooks</b>
            - <b>services</b>
            - <b>index.js</b>
                1. all things we want use from authentication 
                2. only import from this file, all other files export should be in this file
                3. encapsulation of all logic in single location
                4. easy adding new folders
            - <b>...</b>
        - <b>settings</b>
        - <b>...</b>
        1. all code features
        2. replica of the src code excluding features folder
        3. duplicating project structure so everything is reliable
        4. 90% of all code should be in this folder
        5. here is all code that is not global
    - ##### hooks
    - ##### layouts
        - <b>Navbar.js</b>
        1. layouts (components) that are used multiple times accros the page
    - ##### lib
        1. 3rd party libraries, facade pattern putted on top of library 
        2. update only one file of library to update whole library
    - ##### pages
        - <b>Home</b>
            - <b>HomeContent.js</b>
            - <b>TodoForm.js</b>
            - ...
        - <b>Login</b>
        - ...
        1. components that are used only in that page
    - ##### services
    - <b>login.js</b>
    1. services for API
- ##### utils
    - <b>formatDate.js</b>
    1. utility files
    2. small code, simple function, pure functions
- package-lock.json
- package.json