# cypress-example-todomvc-redux [![CircleCI](https://circleci.com/gh/cypress-io/cypress-example-todomvc-redux.svg?style=svg)](https://circleci.com/gh/cypress-io/cypress-example-todomvc-redux) [![renovate-app badge][renovate-badge]][renovate-app] [![Coverage Status](https://coveralls.io/repos/github/cypress-io/cypress-example-todomvc-redux/badge.svg?branch=master)](https://coveralls.io/github/cypress-io/cypress-example-todomvc-redux?branch=master)
> TodoMVC example with full e2e test code coverage

This example is a fork of the official [Redux TodoMVC example](https://github.com/reduxjs/redux/tree/master/examples/todomvc) with a set of [Cypress.io](https://www.cypress.io) end-to-end tests. The tests run instrumented application code and the code coverage is saved automatically using [cypress-istanbul](https://github.com/cypress-io/cypress-istanbul) plugin.

## Install and use

Because this project uses [Parcel bundler](https://parceljs.org) to serve the web application, it requires Node v12+.

```shell
npm ci
npm test
```

The full code coverage HTML report will be saved in `coverage`. You can also see text summary by running

```shell
npm run report:coverage:text
```

## How it works

Application is served by [Parcel bundler](https://parceljs.org) that uses [.babelrc](.babelrc) file to load [babel-plugin-istanbul](https://github.com/istanbuljs/babel-plugin-istanbul) plugin. This plugin instruments the application source code. During tests [cypress-istanbul](https://github.com/cypress-io/cypress-istanbul) merges and saves application code coverage information, rendering the full HTML report at the end.

Unit tests like [cypress/integration/selectors-spec.js](cypress/integration/selectors-spec.js) that reach into hard to test code paths are also instrumented using the same [.babelrc](.babelrc) file, and this additional code coverage is automatically added to the application code coverage.

### .babelrc

To always instrument the code using Babel and [babel-plugin-istanbul](https://github.com/istanbuljs/babel-plugin-istanbul) one can simply use the `istanbul` plugin

```
{
  "plugins": ["istanbul"]
}
```

But this will have instrumented code in the production bundle. To only instrument the code during tests, add the plugin to the `test` environment and serve with `NODE_ENV=test`

```
{
  "env": {
    "test": {
      "plugins": ["istanbul"]
    }
  }
}
```

Parceljs note: there are some issues with environment-specific plugins, see [PR #2840](https://github.com/parcel-bundler/parcel/pull/2840).

### Read

- [Code Coverage for End-to-end Tests](https://glebbahmutov.com/blog/code-coverage-for-e2e-tests/)
- [Code Coverage by Parcel Bundler](https://glebbahmutov.com/blog/code-coverage-by-parcel/)
- [Combined End-to-end and Unit Test Coverage](https://glebbahmutov.com/blog/combined-end-to-end-and-unit-test-coverage/)

The official Cypress documentation guide to code coverage is coming, follow issue [#1705](https://github.com/cypress-io/cypress-documentation/issues/1705)

## CircleCI

Code coverage is saved on CircleCI as a test artifact. You can view the full report there by clicking on the "Artifacts" tab and then on "index.html"

![Code coverage artifact](images/circle-report.png)

The report is a static site, you can drill into each folder to see individual source files. This project should be 100% covered by Cypress tests:

![100% code coverage](images/100.png)

## Warning

Full code coverage is not the guarantee of exceptional quality. For example, the application might NOT work on mobile viewport, while working perfectly on desktop with 100% code coverage. See [cypress/integration/viewports-spec.js](cypress/integration/viewports-spec.js) for how to test main user stories across several viewports.

## License

This project is licensed under the terms of the [MIT license](/LICENSE.md).

[renovate-badge]: https://img.shields.io/badge/renovate-app-blue.svg
[renovate-app]: https://renovateapp.com/
