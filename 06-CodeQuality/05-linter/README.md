## Automated Linters

Linters are tools that can automatically check the style of your code and make improving suggestions.

The great thing about them is that style-checking can also find some bugs, like typos in variable or function names. Because of this feature, using a linter is recommended even if you don't want to stick to one particular "code style".

Here are some well-known linting tools:

- [JSLint](http://www.jslint.com/) -- one of the first linters.
- [JSHint](http://www.jshint.com/) -- more settings than JSLint.
- [ESLint](http://eslint.org/) -- probably the newest one.

All of them can do the job. The author uses [ESLint](http://eslint.org/).

Most linters are integrated with many popular editors: just enable the plugin in the editor and configure the style.

### TODO
* Watch this video https://youtu.be/hppJw2REb8g
* Install [Node.js](https://nodejs.org/) if you don't already have it installed
* Install ESLint with the command `npm install -g eslint` (npm is a JavaScript package installer)
(See <http://eslint.org/docs/user-guide/getting-started> for more details about installation)
* Create a config file named `.eslintrc` in the root of your JavaScript project (in the folder that contains all your files)
* Run ESLint on any JavaScript in your project (if there isn't any yet, don't worry - we will be creating some soon)
* If there are any issues, try to fix them

Here's an example of an `.eslintrc` file:

```js
{
  "extends": "eslint:recommended",
  "env": {
    "browser": true,
    "node": true,
    "es6": true
  },
  "rules": {
    "no-console": 0,
    "indent": ["warning", 2]
  }
}
```

Here the directive `"extends"` denotes that the configuration is based on the "eslint:recommended" set of settings. After that, we specify our own.

It is also possible to download style rule sets from the web and extend them instead. See <http://eslint.org/docs/user-guide/getting-started> for more details about installation.

Also certain IDEs have built-in linting, which is convenient but not as customizable as ESLint.

### [Next Section >>>](../06-testing-mocha)