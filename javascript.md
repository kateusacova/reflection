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

