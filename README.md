# jest-karma-angular-demo

Demonstrates how to run Jest tests on browsers using Karma.

## How to run

```sh
# install dependencies
$ yarn

# Run tests with Jest
$ yarn test

# Run tests with Karma on browsers
$ yarn karma
```

The example Angular project was copied from [jest-preset-angular](https://github.com/thymikee/jest-preset-angular).

## How does it work

The basic configuration for Karma is almost same with what Angular CLI auto generates for Karma/Jasmine.
The only difference is the following lines in [test.ts](src/test.ts), which is run by Karma at the beginning of the test.

```ts
window['jest'] = require('jest-mock');
window['expect'] = require('expect');

// if you are using snapshot testing
window['expect'].extend({
  toMatchSnapshot: () => ({ pass: true })
});

// corresponds to setting `restoreMocks: true` in Jest config
beforeEach(() => jest.restoreAllMocks());
```

The first two lines are always required to run Jest test code on browsers.

If you are using snapshot testing, you have to stub snapshot related methods with `expect.extend()` as snapshot testing depends on `fs` and cannot be run on browsers.
Alternatively, you may be able to enable snapshot testing on browsers by using [`fs-remote`](https://www.npmjs.com/package/fs-remote) if it's worth it.

If you set `resetModules`, `clearMocks`, `resetMocks`, or `restoreMocks` in your Jest config, you have to call the corresponding function(s) in `beforeEach` (see https://github.com/facebook/jest/blob/c24f75191ef09bb72018f3649d1590cfca24b163/packages/jest-jasmine2/src/index.js#L95-L115).

## Limitation

Module mocking is not available.
