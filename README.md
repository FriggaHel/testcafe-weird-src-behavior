# TestCafe src() behaviour demo

This example is derived from [saucelabs-training/demo-js](https://github.com/saucelabs-training/demo-js/blob/master/testcafe/) repository

## Actual behavior

```
$> npm run test.buggy

> testcafe-weird-src-behaviour@1.0.0 test.buggy /Users/felix/Projects/testcafe-weird-src-behaviour
> node tests/configs/buggy.config.js

 Running tests in:
 - Chrome 86.0.4240.198 / macOS 10.15.7

 Test Login
 ✓ should be able to test loading of login page
 ✓ should be able to login with a standard user
 ✓ should not be able to login with a locked user

 Test Login
 ✓ should be able to test loading of login page
 ✓ should be able to login with a standard user
 ✓ should not be able to login with a locked user


 6 passed (14s)
Tests failed: 0
$>
```

## Expected behaviour

```
$> npm run test.expected

> testcafe-weird-src-behaviour@1.0.0 test.expected /Users/felix/Projects/testcafe-weird-src-behaviour
> node tests/configs/expected.config.js

 Running tests in:
 - Chrome 86.0.4240.198 / macOS 10.15.7

 Test Login
 ✓ should be able to test loading of login page
 ✓ should be able to login with a standard user
 ✓ should not be able to login with a locked user


 3 passed (14s)
Tests failed: 0
$>
```

## Explanations

Both configurations are slightly different:
- Buggy:
    ```js
          .src([
            'tests/specs/',
            'tests/specs/login.spec.js',
          ])
    ```

- Valid
    ```js
          .src([
            'tests/specs/login.spec.js',
            'tests/specs/login.spec.js',
          ])
    ```

Since there is globing applied on directories, glob is resolved after de-duplication.\
In valid behaviour, specs is ran only once, in buggy, several times.
