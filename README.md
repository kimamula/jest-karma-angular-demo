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
window['expect'].extend({
  toMatchSnapshot: () => ({ pass: true })
});
```

The first two lines are always required to run Jest test code on browsers.
Additionally, if you are using snapshot testing, you have to stub snapshot related methods with `expect.extend()` as snapshot testing depends on `fs` and cannot be run on browsers.

That's it.
