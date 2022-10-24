# JavaScript

### Definitions

**Asynchronous behaviour**
- any behaviour that takes a non-trivial amount of time to complete
- e.g. **callback** function passed as argument to `setTimeout` function to be executed after the delay 
- e.g. to handle API response

**Document Object Model (DOM)**
- allows JS interaction with web page elements
- representation of different elements and their hierarchy



Something to explore later:
Arrow function

### Tools

**esbuild**
- build tool
- composing together all the files needed to be load on the page 
- so that you can put in the script tag only one file: bundle.js

**Node.js**
- backend runtime environment
- to build command line tools
- & for server-side scripting to build dynamic web page

### JS Project Setup
```
nvm use node # set up environment for the latest node
npm init -y # initialize npm project creating package.json
npm add jest # for TDD
npm install -g jest # to run jest command
npm install -g esbuild # to compose files
touch index.js
touch index.html
```

```js
// in package.json
"build": "esbuild index.js --bundle  --outfile=bundle.js --watch" // to: npm run build

```
```js
// in index.html
! // to ouput DOCTYPE by VSCode
<script src="bundle.js"></script> // to run the composed files
```

### Testing DOM Updates

```js
// if error, run  npm i jest-environment-jsdom --save-dev

/**
 * @jest-environment jsdom
 */

const fs = require('fs');
const View = require('./view');

describe('A test for my web page', () => {

  // We can use the beforeEach() hook 
  // to set the jest `document` HTML before each test
  beforeEach(() => {
    document.body.innerHTML = fs.readFileSync('./index.html');
  });

  it('displays a title', () => {
    // 1. Arrange - instantiate our View class
    const view = new View();

    // 2. Act - call any method that modifies the page
    // this method `displayTitle` would dynamically
    // set a <h1> title on the page with the given content
    view.displayTitle('My amazing website');

    // 3. Assert - we assert the page contains what it should.
    // Usually, you will use `.querySelector` (and friends)
    // here, and assert the text content, the number of elements,
    // or other things that make sense for your test.
    expect(document.querySelectorAll('h1').textContent).toBe('My amazing website');
  });
});
```

