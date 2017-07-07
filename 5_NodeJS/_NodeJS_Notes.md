# Node.js 

| #   | Topic                                               | Date       | Lecturer |
| --- | --------------------------------------------------- | ---------- | -------- |
| 1.  | [Course Intro ](#intro)                             | 20.June | Doncho   |
| 2.  | [Course Project Requirements](#intro)               | 20.June | Doncho   |
| --  | [Node.js Overview](#overview)                       | 20.June  | no video |
| 3.  | [Modules](#modules)                                 | 20.June | Doncho   |
| --  | [Asynchronous Operations](#asynchronous-operations) | 22.June | no video |
| --  | [File Databases](#file-databases)                   | --         | --       |
| 4.  | [Live demo Web crawler](#web-crawler)               | 22.June | Doncho   |
| 5.  | [Unit Testing](#unit-testing)                       | 27.June | Doncho   |
| 6.  | [Tooling](#tooling)                                 | 27.June | Doncho   |
| 7*  | [Express Pug & Passport](#express-pug-passport)     | 29.June | Doncho   |

# Intro
_20.06.2017 - Doncho_

1.  ## Topics

    - File IO we'll use for practising **async calls** - 5 types (promises - most widely used, callbacks, observables, yield, async/await from ES2017).

    - Debuggers, tools task runners (gulp) - set-up. Task runners - **Gulp** - used for automation, we set-up operations, create requests and it runs them (eg. automate compile/build sass to css, ES2015 to ES5). 

    - Databases - MongoDB.

    - Web development - **Express** framework for Node.js (like ASP.NET for C#, Jango for Pyton, SpringMVS for Java, Laravel and CodeIgniter for PHP). Provides convenient way to create apps quickly. Will talk about MVC-like (pure MVC in javascript is a huge overhead and not worth it). MVC = architecture pattern for creating  multi-layered applications. Goal is to structure apps to be reusable, testable, and easy to extend and add new functionality.

    - **WebSockets** - AJAX = way for creating HTTP requests to web servers and receiving responses. WebSockets provide a way for the server to ping the client (eg. chat clients, notifications), so that the client doesn't have to explicitly requests to the server, two-way client-server communication.

    - **UT** in Node.js with javascript - **Mocha** framework with Chai syntax. Functional testing - also with Mocha & Chai - launches page and clicks around it checking for correct result. Have a browser object with which we manage the browser (something like jQuery).

    - **Containers** - isolated environment with automatic set-up of specific installed program versions and tools. Something like a virtual machine.

    - **Cloud** - Amazon Web Services (AWS) - launch instance, deploy. Has free trial.

2.  ## Course project
    
    (in intro and in separate video)

    Standard web app not SPA and AJAX only, AWS hosting. Use Node.js, Express, MongoDB.

    !**ESLint - zero errors** - custom config rules.

    Additional tasks to solve during project presentation.
    
    Public and private parts.

    - BACK-END - 40%

        **Pug** == ex. Jade - rendering engine similar to Handlebars (also accepts a javascript object), no closing tags, significant whitespace (whitespace sensitive, tabs are important for nesting).  . (dot) is very important at the end of  line signifying that you can have text on the next line. Supports reusable components - extension/inheritance of templates and mix-ins (eg. navigation is in another file and called as function). HTML is cleaner and easier for navigation.

        Node.js & Express can work with other rendering engines (i.e. Handlebars).

        **REST** (get, post) routes to load components with AJAX (eg. creating new post can use AJAX to load the drop-down with categories). Also private (authenticated) route - **token**  authentication (web app auth).

        Authentication - must be both session and token

        **MongoDB** - fast search, slow insert, no relations

        **Data/service layer** to abstractly access the data storage. Needed for UT.

        **Passport** - for authentication and managing users. Hard to set up but documentation has good instructions.

        **WebSockets** - Socket.io (computer communications protocol, providing full-duplex communication channels over a single TCP connection).

    - FRONT-END - 25%

        !**Usability** over design. Any framework is allowed (KendoUI, AngularJS, Angular 2, Knockout, Bootstrap). Responsive design required.

        Communication - AJAX and/or WebSockets.

        Handle errors and validate data to avoid crashes. Use loaders and notifications.

        Security - Escape values coming from user input fields. 

    - TESTS - 25%

        A **sample application** with UT, integration and functional automation tests. **Doncho will provide link to it**!

        **Yarn** = alternative to npm, wraps npm and makes it faster. Builds a tree of dependencies, installs them in parallel. Npm is linear which makes it slower.        

        Test **database needs to be cloud hosted** but run tests *locally*! In real-life projects this would be part of continuous integration which runs tests on every commit. The code which launches the app and creates a database should not be in the UT file. At this stage can't talk about *CircleCI*, **Jenkins** and other tools which automate this process. Maybe in the ASP.NET maybe. The solution we use works with **Selenium** which uses the browser to conduct tests -> uses the DOM tree. For mobile devices there is no DOM tree and other tools are used.

        **Test back-end** (UT - Mocha, Chai), not frontend (which is not expected to have very thick logic) - 50% code coverage - **Istanbul.js** tool for code coverage.
        
        **Integration/Functional** automation tests required too (Not continuous integration - which tests on every commit). Use web driver for FireFox or Chrome in **Selenium**. Browser *phantomjs* is headless Chrome, older, uses webkit, not blink, works in background. Test 50% of application routes for authenticated and non-authenticated users.

        Integration test for AJAX routes will be optional.

    - Deployment in Amazon Web Services (AWS) - 10%

    - BONUS - 10%
        
        - Continuous integration - Jenkins, CircleCI, etc. - can be set up at the end when we are  ready with the application.
        - UT client code
        - Containers
    .

3.  ## Tools

    - OS: Windows, Linux, Mac - Node.js is not perfect in Windows (launches slower), was designed for Linux initially.
    - Text editor: VS Code preferred 
    - Node.js version: v.8+
    - Server: MongoDB 
.

# Overview
_20.06.2017 - Doncho_

1. ## Node.js Overview
    - What

        Initially Node.js was V8 webkit Chrome engine mocked to work on server.

        Other platforms on which to write js to run on server:

        Rhino - similar to Node.js specialized for image processing

        React native & Native script are something similar, similar flow

        Node.js + Express = web development

    - How

        Event-driven - event loop distributes operations
        
        Single-threaded - libuv allows async operations

    - **Event loop** (*learn more)

        V8 = browser without UI

        Node.js bindings - javascript to C++, create events

        Libuv (= middle man to the OS) - Event queue - queues all async operations - event loop sends them to the OS. while the OS is completing this operation, the event loop does nothing, if all threads are busy. When a thread slot is freed, the event loop returns the execute callback to the event queue and takes the next operation in the queue.

2. ## Setup    
    
    **Installation:**


    - Standard installation - install from website, check if added to $PATH. Not so flexible for development because only one version of Node.js is possible.

    - Using NVM (Node Version Manager) - should be installed to C:\nvm (no whitespace and special characters). Allows update of Node.js as often as needed, also allows testing on different versions of Node.js.

    Node.js v8+ supports keywords async and ??

    **IDEs:**

    - **VS Code** 
        - intellisense gives some information - uses TypeScript (by Microsoft = superset to JavaScript; Java compiled to JavaScript; strongly typed JavaScript). Comes from d.ts files with meta data about the code. Not all libraries have these typings.

        - !Plugins: 
        
        **Auto Import 1.2.2** - observable import, works with TS not always with JS.

        **CSSLint, ESLint** - file .eslitrc - *Doncho will add it to the demos

        **Path Autocomplete / Path Intellisense**
    
    - Atom
    .

    **Async vs. multi-thread programming:**

    - Async - don't care how the operation is completed, less control

    - Multi-thread - more control, threads are created by the developer and, when completed, must be taken care for something from the main thread to call them back and identify what kind of data main will have access to, otherwise data in the main thread could be modified by other threads.

    **Shortcuts**

    **Ctrl + Space** = possible options

.

# Modules
_20.06.2017 - Doncho_

1. ## Modules in Node.js

    - **Scope**

        Issues with global variables in JavaScript - solved with IIFEs which create function scope.

        In Node.js **global scope is explicit** - have to specially define variables which belong to it. Every file is a node.js module. Variables by default are accessible only in the file they are declared in. Solves issues with global variables.

        Modules in Node.js are different parts of an application (like classes in C#). Useful for splitting the code into smaller pieces.

2. ## Loading modules

    **Build-in modules** (ie. modules which come with Node.js) are loaded with their name.

    `require(path_to_module)` - (like `using` in C#) - global function Node.js, loads exports from the respective module (eg. 

    `/* globals globalVarName */` - to resolve ESLint underlining global variables coming from other modules.
    
    ```js
    /* globals __dirname */
    const fs = require("fs") //fs = file system 
    // read all files from directory
    fs.readdirSync(__dirname)
        foreach((file) => ){
            console.log(file);
        }
    ```

    **Third party modules** are loaded with `require("path/moduleId")`;

    Modules which we define - the id is the relative/absolute path to the file location. Always use `./` when referring to current directory.

3. ## Exporting 

    `module` - another global object (like `exports`, `require`) used to handle modules.

    ```js
    // file printer.js
    const print = (msg) => {
        console.log(msg);
    }

    module.exports = {
        /* like IIFEE, list functions to export */
        print
    }
    
    // file app.js
    const printer = require('./utils/printer'); //printer, not printer.js
    ```
    
    - Using **exports** - not recommended: 
    ```js
    // file printer.js
    /* globals exports */ // for option 2
    const print = (msg) => {
        console.log(msg);
    }

    exports print = print;
    
    // file app.js
    const printer = require('./utils/printer'); 
    ```
    
    - Using **global** scope (not a good practice) - not recommended:
    ```js
    // file printer.js
    /* globals global */ 
    const print = (msg) => {
        console.log(msg);
    }

    global.print = print;
    
    // file app.js
    const printer = require('./utils/printer'); //?must it be assigned?
    
    const print3 = global.print;
    ```

    Global scope could be useful if using Node 4 where no promises exist, to attach an external library:
    ```js
    global.Promise = require('bluebird');
    ```

    - If using **classes**, the module could export the class itself or a function which creates an instance of the class (be consistent, use one of the two export options). JavaScript is more interested in the _properties_ of objects (duck typing). Classes in js are syntactic sugar for prototypal inheritance. Using `instanceof` is an anti-pattern because it breaks _duck typing_.
    ```js
    class Printer{
        print(msg){
            console.log(msg);
        }
    }

    module.exports{
        Printer,
        getPrinter(){
            return new Printer();
        }
    }
    ```

    `Export` and `import` from ES2015 are not supported in Node.js yet. 
         
        
4. ## Importing functions (reading modules)
    
    Using .js extension when requiring modules is optional.
    
    ```js
    const printerModule = require('./utils/printer');
    let Printer = printerModule.Printer;
    let printer = printerModule.getPrinter;
    ```

    - Using **destructuring assignment** to import (use new line for each property for better readability)

    ```js
    /* file app.js */
    const { 
        getPrinter, 
        Printer 
    } = require('path to module');
    ```

    - **Index.js** file/module - default module for the folder - can be imported with only the folder name, without the file name. Useful for automatic loading of all the modules in the folder. 

    > In index.js only `require` files with the implementation logic, name them with the same name as the folder.

    ```js
    require('folder name');
    ```


5. ## Using third-party modules 
    (eg. Nuget, Bower, Fetch) - installed with NPM or Yarn also required only with the name of the module.

    > browse [npmjs.com](https://www.npmjs.com/)
    
    - **Fetch** - api from browser (from HTML5) which replaces the XHR object - makes HTTP requests easier, native to JavaScript, works with promises. Because it's not part of the JavaScript standard, it's not accessible in Node.js. But can be downloaded and installed with NPM.  
        
    ```js
    const fetch = require(node-fetch);

    fetch('http://localhost:3001/api/superheroes')
        .then((response) =>{
            return response.json();
        })
        .then((result) => {
            console.log(result);
        });
    ```
    
    `npm node-fetch --save` - installs the module in the current directory. Must have package.json file to be saved as a dependency.

    `npm init -y` - creates package.json file -y = yes to skip questions. Node.js projects are folder-based - all subfolders are part of the project (not like in C# - solution, project, references, etc.). The package.json file stores meta data about the project, including dependencies which can be restored easily on other computers.

    `npm install` - recreates/restores dependencies saved in package.json

    `npm install -g http-server` - installs globally

    `npm install --save-dev packageName` - saves as development dependencies
    
    `npm uninstall --save-dev packageName`

    - **Yarn** (npm package) - makes npm work better. Does topological sort of the dependencies = resolves dependencies and installs them in parallel instead of synchronously = faster than npm install. Must be installed globally.

        `npm install -global yarn` - installs in node/[version]/lib/node_modules. Global packages can be used from any node project. If node.js version is updated (with NVM), global modules need to be reinstalled in the new version folder.

        `yarn add eslint` - automatically adds dependencies in package.json

        `yarn global add http-server`
        
        `yarn global add http-server -dev`

        `yarn global remove http-server`

        `yarn init -y` - initialise project with package.json

        `yarn` = npm install
.

# Asynchronous Operations
_22.06.2017 - Doncho_

1. # Intro

    Always initialise a project with `npm init -y` (or `yarn init -y`?)

    **Package.json**

    **index.js**
    
    `"scripts": { "start": "node app.js" }` - Defines what to do on `$ npm start`. Accepts all valid power shell and bash scripts/commands.

    `cygwin` = bash for windows

    `power shell` =  bash for windows; script language allowing automation of commands
    
    Custom commands:

    `"scripts" { "dev": "nodemon app.js" }` - restarts server? Nodemon package - screens changes to files (install global).

    `$ npm run dev` - run custom commands  

    `"main": {"fileName.js"}` - main script - Defines startup/entry point of the application with `node .` (optional, mainly used for npm packages)

    .eslintrc - dot signifies hidden files in Linux

2. # Overview

    Node.js is single-threaded but the event loop is not. Operations can be run asynchronously - passed to the event queue of the event loop. When an async operation is ready, it fires an event handler.

    Various practices:

    - **callbacks** - most popular, because they come from javascript and have been around for years. The problem with them is that they cause long nesting chains ("the pyramid of death"). Very difficult error handling.

    - **promises** - good option - provide easy way to avoid nesting of async operations. Easy error handling (`.catch` at the end)

    - **observables** - external library - RxJS library (reactive extensions). Introduce functional principles of programming, works better with javascript.

    - **yield + function generators** = hack, can be used for handling async operations as a side effect. Overhead for small projects.

    - **async + await** - work with/like promises but can be used easier, ES2017?


3. # Callbacks
4. # Promises

    Promises flatten callbacks = better chaining.
    resolve and reject are callbacks. Other callbacks - err, loading?

    ```js
    let pr = new Promise((resolveCb, rejectCb) => {
        //async operation
    });

    const waitSeconds = (seconds) => {
        return new Promise((resolve, reject) => {
            setTimeout(resolve, seconds * 1000)
        });
    };
    ```

    ```js
    waitSeconds(2).then(() => {
        //success
    }, () =>{
        //error
    })
    .then(() => {
        console.log('1. It works');
        return waitSecodns(2); 
        // if return waitSeconds is missing, 
        // the following then-s will not wait 2 seconds more 
        // but just print right away
    })
    .then(() => {
        console.log('2. It works');
        return waitSeconds(2);
        //
    })
    .catch(() =>{
        // Doesn't have to be at the end of the block.
        // Every promise has then & catch functions
    };

    ```

    Promise all - takes an array of promises and runs after all of them are completed. Then also returns a promise.

    ```js
    Pormise.all([
        waitSeconds(1)
            .then(() => console log('1')),
        waitSeconds(2)
            .then(() => console log('2')),
        waitSeconds(3)
            .then(() => console log('3')),
    ])
        .then(() => {
            console.log('All are ready');
        });

    ```

    ```js
    //Creates a resolved promise which can be chained
    Promise.resolve()
        .then((result) => {
            console.log(result);
            //prints undefined
            return 1;
        })
        .then((result) => {
            console.log(result);
            //prints 1
            return Promise.resolve(1);
        })
        .ten((result) =>{
            console.log(result);
            //prints 1 too
        })
    ```

    ```js
    Promise.all([
        Promise.resolve(1),
        Promise.resolve(2),
        Promise.resolve()
    ])
        .then((results) => {
            console.log(results);
            //logs in reverse order ?
        })
        .then(([r1, r2, r3]) =>{
            //destructuring assignment
            console.log(r1);
            console.log(r2);
            console.log(r3);
        })

    ```


5. # Async & await

    Work with promises. Need to create an async function to use them. Similar to C# (...)

    Defining

    ```js
    const f = async() =>{

    }
    ```
    ```js
    async function f1(){

    }
    ```
    ```js
    let obj = {
        async f3(){

        }
    }
    ```
    ```js
    class Person {
        async load(){

        }
    }
    ```

    Similar to the then-s but code is even more linear.

    ```js
    const f = async () =>{
        await waitSeconds(1); 
        // waits for this function to complete 
        // before moving to the next one
        console.log('1.');
        await waitSeconds(2);
        console.log('2.');
        const result = await waitSeconds(3);
        //to get  result just assign the await function to a var
        console.log('3.');

    }
    ```

    To be able to use await, we have to be in a method marked as async.

    ```js
    const asyncOperation = async (param) => {
        await waitSeconds(2);
        console.log ('Ready' + param);
        return param;
    };

    const main = async () =>{
        const result = await asyncOperation(5);
        console.log(result);
    }

    main();
    ```

    Await & async are syntax sugar to promises.

    ```js
    const f1 = async() => {
        return await 5;
        return await Promise.resolve(5);
        // returns the result wrapped in a promise
        // both are the same thing
    }
    ```

    Allow try-catch block similar to all other languages, instead of calling callbacks

    ```js
    const main = async () => {
        try{
            const result = await asyncOperation(5);
            console.log(result);
        }
        catch (err){
            console.log(err);
        }
    };
    ```

6. # Observables

    ```js
    const {Observable} = require('rxjs');
    ```

    Can continuously provide data. We attach a callback which fires every time...?

    Used similarly to promises.

    ```js
    const waitSeconds = (seconds) => {
        return Observable.
            create((o) =>{
                o.next();
            })
            .delay(seconds * 1000);
    };

    waitSeconds(1)
        .do(()=>{
            console.log('1.');
        })
        .delay(1000)
        //same as subscribe
        .subscribe(()=>{
            //instead of then
            console.log('1.');
        });
    ```

    ```js
    const tick = (tickPeriod) =>{
        return Observable.create((o) => {
            setInterval(() => {
                o.next();
            }, tickPeriod * 1000)
        });
    };

    let index = 1;
    tick(1)
        .subscribe(() => {
            console.log(index);
            index += 1;
        })

    // prints out continuous numbers.
    ```

    Observables (for the moment) don't provide anything new compared to promises. Angular2 works with observables.

    Can't be used because not implemented everywhere yet?

7. # Yield & generators

    Do something like async. Too complicated.
.

# File Databases
_== The live demo?_

# Web Crawler
_22.06.2017 - Doncho live demo_

0. Using:
    - Promises - Async programming
    - Http
    - Modules
    - IO - LoweDB file database
    - DSA - queue, DFS

    Source: Goodreads.com public data, IMDB

1. Steps:
    1. Get data
        - Http -> html
        - HTML -> objects
    2. Save data

2. Libraries:
    - **isomorphic-fetch** - better than node-fetch because can be required once, attaches `fetch`, `Response`, `Headers`, `Request` to global scope, can be used everywhere; futuristic
    - **jquery**
    - **jsdom**

3. History of Node.js
    - Node start (2009)
    - phantomjs - headless browser, old Chrome working with webkit (not with blink) used for image processing and automation of testing 
    - HTML5 (new HTML + extended JS and CSS)
    - Node 0.10
    - Split to Node 0.11,12,13,14 and IO.js = forked Node.js with added new features - lambda, classes - v.1,2,3
    - Merge two forks to Node.js 4.X

4. Process:
   
    -  Set up **eslint**: `npm install -g eslint eslint-config-google babel-eslint`, add rule about line breaks `rules{"linebreak-style": ["error", "windows"]}`, configure VSCode to add empty line at the end of file (issue with JS-CSS-HTML Formatter extension - change to true "end_with_new_line")

    > Have only config files in the main directory and main.js- split js files to folders

    - `$ npm init` -> package.json file
    - `$ yarn add isomorphic-fetch` - create folder 'polyfills' with index.js `require('isomorphic-fetch')`, in app.js `require('./polyfills');`
    - define/import url to use - can hard code values of genres to crawl in an array (or program crawler to extract genres from genres list from the website)
    - `$ node app.js > result.html` - output to file instead of the console
    - parse received html data to json
    - `yarn add jquery` jQuery is a JavaScript library for DOM manipulation but could be used on server side too, not only client side.
    - `yarn add jsdom` - simulates DOM tree - enables use of $ in Node. Check instructions at npmjs.com jQuery and jsdom. Create folder 'dom-parser' with 
    index.js `module.exports = require('./dom-parser.js');` 
    file dom-parser.js `const jsdom = require('jsdom');` and implementation logic function exporting the '$'.
    - find selectors from the returned html result and parse title and poster img url of movie.

    > Better always return promises even for synchronous operations = consistency

    - Create folder 'models' with 
    movie.model.js defining class Movie with constructor
    movies.extensions.js - move parsing logic there dynamic add static method to the movie class
    `Movie.prototype.newMethod = () => {}` - instance method
    `Movie.newMethod` - static method;

    - Create folder 'parsers' and move getMovieData from app.js
    - Create genre parse logic
    - Make extensions load dynamically - now we don't need to add new extensions explicitly
    - Get list of movies ids from genres in an array
    - Create queue to replace the array - don't need classes for it - we need an object with the certain properties, but we don't always need to create a class for that. Classes in js are used only when inheritance is needed.

.

# Unit Testing
_27.06.2017 - Doncho_

1. # UT Frameworks - quick review

    UT = Test one module/one file.

    - JSUnit - rarely used, based on JUnit for Java
    - QUnit - created by John Resik (creator of JQuery), mostly used for front end testing
    - **Jasmine** - largely used
    - **Mocha** - more powerful than Jasmine, largely used; flexible, pluggable framework - accepts additions. Needs syntax for creating UT - assert, should, expect. Most popular syntax library - **Chai**. `Should` extends the object prototype and adds method should to all objects. `Expect` is mostly used because it's most expressive.

    ```js
    assert.areEqual(expected, actual);
    expect(actual).to.be.eql(expected); // only value ==
    actual.should().equal(expected); // absolute ===
    ```

2. # Demo

    - Initialise: `yarn init -y`

    - Install as dev dependency. Testing is not part of the development process but in dev should put everything we don't want to be in the production: `yarn add mocha chai --dev`

    - Create 'test' folder and file 'simple.test.js' for the tests

    - Load expect: `const { expect } = require ('chai');`

    - Create a simple test with `it('test name', () => {//AAA})`: 

    ```js
    it('should return 4', () => {
        // Arrange
        const x = 2;
        const y = 2;

        // Act
        const expected = x + y;

        // Assert
        expect(expected).to.eq(4);
    });
    ```

    - Run tests through Mocha 

    `$ mocha test/simple.test.js` if Mocha is installed globally. But that could be inconvenient for other users of the project who don't have global Mocha.
    

     `$ ./node_modules/.bin/mocha test/simple.test.js` is another (also not very convenient) option is to reference bin folder where shortcuts to the locally installed libraries, which are accessible after `$ npm install` (*works in Git bash, not in VS Code terminal): 
   

    **Best**: Add reference to package.json to be able to run with 
    `$ npm test`

    ```js
    "scripts":{
        "test": "./node_modules/.bin/mocha test/simple.test.js"
    }
    ```

    - Group tests into files, or group into test suites(?).

    `describe` statement groups other tests and adds methods:  
    `before` runs before all tests in the current describe block, `after`, `beforeach`, `aftereach`. Describes can be nested - beforeach and afterach apply to the nested statements as well. Can be more than one.
    
    `describe.skip` or `it.skip` - skips a group or test. 

    ```js
    describe('Test group', () =>{
        before(() =>{
            // runs before all tests
        });

        aftereach(() => {
            // runs after each test, incl. nested ones
        });

        describe.skip('Nested', () => {
            it('should return 4', () => {
                // Arrange, Act, Assert
            });

            it('should return 4', () => {
                // Arrange, Act, Assert
            });
        });
    });
    ```

3. # Asynchronous tests

    `It` are async. (?)

    - **Avoid**: with `done` parameter/callback. The test will wait for the `done` callback to be called.

    ```js
    const getValueAfter = (value, seconds) => {
        return new Promise((resolve) => {
            return setTimeout(() => resolve(value), seconds * 1000);
        });
    };

    describe('Async tests', () =>{
        it('with done()', (done) => {
            getValueAfter(5, 1)
                .then((value) => {
                    expect(value).to.equal(5);
                    done(); // !important
                });
        });
    });
    ```

    - **Recommended**: with `promise` (from newer versions of Mocha) - `it` knows that it has been attached a method returning a promise, it should execute it.

    ```js
    describe('Async tests', () =>{
        it('with return promise', () => {
            getValueAfter(5, 1)
                .then((value) => {
                    expect(value).to.equal(5);
                });
        });
    });
    ```

    - Mocha transpiles the test code, then analyses it.

    ```js
    it('without calling a funciton', () => {
        expect(5).not.to.be.null;
    });
    ```

.

# Tooling
_27.06.2017 - Doncho_

0. # List
    - IDEs - **VSCode**, WebStorm, Atom, ViM, etc.
    - Package managers - NPM, Yarn, (Bower)
    - Project scaffolding - **Yeoman**
    - Task runners - **Gulp**, (Grunt, WebPack - Angular2 works with it)
    - Debugging - Node
    - **NodeMon** - automatic app rerun on file change. Will be useful when working with Express because we'll work either in the IDE or in the browser and restarting the server from the console will not be convenient.

1. # Package managers - **Bower**

    - Bower - a npm package

        Used to be used for front end packages

    - NPM - installing locally/globally, adding dev dependencies, initialising apps. 
    
        Used to be used for back-end packages.

    The separation between front-end and back-end was useful. There was a shift to uploading packages only to npm and now Bower is less used.

    Bower - similar API to npm. Only local installs, no global.

    `bower init` - creates 'bower.json' file and 'bower_components' folder

    `bower install --save jquery`

    `bower install` recreates dependencies

    To link to `npm install` and install all bower dependencies, add Bower to devDependencies `yarn add bower -dev`. In package.json add:

    `"scripts" { "postinstall": "bower install" }` - for globally installed Bower

    `"scripts" { "postinstall": "./node_modules/.bin/bower install" }` - for locally installed Bower   

2. # App scaffolding

    - [**Yeoman**](Yeoman.io)

    **Scaffolding** tool for web apps. In Visual Studio like selecting the project type when creating an new project - some files are created automatically - i.e. Console Application, etc.

    `yarn global add yo` or `npm install -g yo` - !?_yarn doesn't work on my computer_

    `yarn global add generator-express` or `npm install -g generator-express`

    `yo express` - starts scaffolding the project - select options. Starts downloading npm packages, creates file system.

    Used **once** when starting a project. Creates very basic projects which are not always the best and need to be changed later.

    `yo` command to look for other generators - eg: asp.net mvc
    
3. # [**Task runners**](https://youtu.be/wet1WNvJ7vA?t=20m54s) - Gulp & Grunt

    - Allow process automation

    Transpiling with Babel can be automated by creating a task runner command.

    Will run all future apps through Gulp. When we create integration tests we'll need a running server or a test database. All these tasks can be automated with test runners. The tests themselves should not create a fake database because this is too much of a responsibility. That's why we could set up task runners to do that.

    Gulp and Grunt do the same thing, achieve the same result but with different means.

    - **Grunt** - the old guy, works well, very stable, is being substituted with Gulp where writing is easier. Hard to configure. Have to pass big js objects for every operation. If we want a stylus css files to be compiled to one minified file, we have to first merge them, then compile them to one file, then minify it. Each of these steps is a separate configuration.

    *  **CoffeeScript** - js preprocessor, written using Python stuff, first use of lambda and classes, curly braces not obligatory for scope, significant whitespace. CoffeeScript is dying out with the development of js but is resurrected by Grunt because reduces configurations length.

    - **Gulp** - more convenient, easier to execute the configurations. The start Gulp file is a standard js file where regular  JavaScript is accepted. 

        `$ yarn init -y`

        `$ npm install -g gulp`

        `$ yarn global add gulp` (problem installing through yarn)

        `$ yarn add gulp` (install locally doesn't work)

        `$ mkdir folderName` - creates folder

        `$ echo.>gulpfile.js` - creates file, `touch gulpfile.js` (Linux)
        
        Gulp uses **streams** (=chaining) which gives better readability, makes configuration easier.

        ```js
        const gulp = require ('gulp'); 
        /* accepts all js code */
        gulp.task('sample', () =>{
            /* do stuff; */
        })
        ```    

        `$ gulp sample` - executes the saved task

        Gulp automates build/compilation process. Can combine several tasks into one. Works with streams.   Stylus, CoffeScript, TypeScript files can be compiled with one command with Gulp. First add plugins for Gulp as local dev dependencies (`yarn add gulp-stylus gulp-babel gulp-typescript --dev`).
    
    * Stylus
    
        ```js
        const stylus = require('gulp-stylus');

        gulp.task('compile:stylus', () =>{
            /* get files any folder down, 
            with extension styl
            !return stream */
            return gulp.src('./app/styl/**/*.styl')
                /* compile */
                .pipe(stylus())
                /* put temp css files in build folder */
                .pipe(gulp.dest('./build/css'));
        });
        ```
        `gulp compile:stylus`

    * Babel

        `yarn add babel-preset-2017 -dev`

        ```js
        const babel = require('gulp-babel');

        gulp.task('compile:es2017', () =>{
            return gulp.src('./app/babel/**/*.js')
                /* set up preset */
                .pipe(babel({
                    presets: ['es2017']
                }))
                .pipe(gulp.dest('./build/es2017'));
        })
        ```

    * Group tasks
    
        ```js
        gulp.task('compile', ['compile:es2017', 'compile:stylus'],
        /* can also pass a callback 
        executes after compilation */
        () => {
        });
        ```

    * Clean tasks - delete old/tmp files
    
        `yarn add -dev gulp-clean`

        ```js
        const clean = require('gulp-clean');

        gulp.task('clean', function(){
            /* delte build folder */
            return gulp.src('./build', 
            /* don't load files to memory */
            {read: false})
                .pipe(clean());
        })
        ```

        Possible issue when using `clean` to delete everything (all old build files) in the dest folder and grouping it with other tasks. Tasks are async and while cleaning, the other tasks in the group could be running and writing. Use clean as a **synchronous** operation or use `gulp-sync` library.

        ```js
        gulp.task('compile', 
            ['clean']),
            () => {
                /* destructuring assignment */
                ['compile:es2017', 'compile:stylus']
                    .forEach((task) => gulp.start(task));
            }
        ```

        * Default task - can be run with `gulp` or `gulp default` command.

        ```js
        gulp.task('default', () =>{

        });
        ```

    * UT
    
        Will start UT through Gulp in the future, it makes sense for integration tests - to launch test server, create database. 

        `yarn add gulp-mocha --dev`

        ```js
        const mocha = require('gulp-mocha');

        gulp.task('test:unit', () =>{
            gulp.src('./test/unit/**/*.js')
                /* optional mocha settings */
                .pipe(mocha({
                    reporter: 'nyan', /* 'dot' */
                }))
        });
        ```
.

# Express Pug & Passport
_29.6.2017 Doncho_ *missed class

.