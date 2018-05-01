# babel-7-out-dir-does-not-preserve-dir-structure-bug

## Expected result

Running `npm run babel` should start a babel watch session where files are compiled to the `lib` directory while preserving the directory structure of `/src` initially, and consistently after file changes, like this:

```bash
$ npm run babel

> babel-7-out-dir-does-not-preserve-dir-structure-bug@1.0.0 babel E:/repos/babel-7-out-dir-does-not-preserve-dir-structure-bug
> babel --watch --out-dir lib **/*.jsx --verbose

src/App.jsx -> lib/App.js
src/utils/index.jsx -> lib/utils/index.js
🎉  Successfully compiled 2 files with Babel.
src/App.jsx -> lib/App.js
src/utils/index.jsx -> lib/utils/index.js
```

## Actual result

The first compilation outputs the files at the root of the `out-dir` directory, while any subsequent compilations triggered by changed files land at a different location.

```bash
$ npm run babel

> babel-7-out-dir-does-not-preserve-dir-structure-bug@1.0.0 babel E:/repos/babel-7-out-dir-does-not-preserve-dir-structure-bug
> babel --watch --out-dir lib **/*.jsx --verbose

src/App.jsx -> lib/App.js
src/utils/index.jsx -> lib/index.js
🎉  Successfully compiled 2 files with Babel.
src/App.jsx -> lib/src/App.js
src/utils/index.jsx -> lib/src/utils/index.js
```
