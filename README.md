# rollup-plugin-rewrite-imports

Pass a string in to rewrite the path of ES module imports and dynamic imports if the dependency already exists in a separate node_modules directory.

## Why

This is useful when you have fragmented or disconnected build routines. This can happen
when part of 1 application is modularly mixed with another at run time. [HAXcms](https://haxtheweb.org)
leverages this plugin to allow theme developers to use the expeced approaches and methods
they typically find in web component development, yet not break the site given that
the build routine is shipped with that system.

This puts theme developers and platform owners on the same tooling / workflows yet
work independently of one another.

## Install

```
$ npm install rollup-plugin-rewrite-imports --save-dev
```

or

```
$ yarn add rollup-plugin-rewrite-imports --dev
```

## How to use

`rewriteImports` is called in order to forcibly point to the location that we are
actually building these assets into.

```javascript
const path = require("path");
const autoExternal = require("rollup-plugin-auto-external");
const rewriteImports = require("rollup-plugin-rewrite-imports");
const production = true;
module.exports = function() {
  return {
    input: "src/custom.js",
    treeshake: !!production,
    output: {
      file: `build/custom.amd.js`,
      format: "esm",
      sourcemap: false
    },
    plugins: [
      rewriteImports(`../../build/es6/node_modules/`)
    ]
  };
};
```
