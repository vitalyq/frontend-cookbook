# Test Front-End JavaScript

While running tests in Node.js is sufficient for most server-side modules, testing browser code in Node.js is not enough in most cases. We suggest these testing strategies depending on the project type:

| Project Type | Test Types | Runtime |
| --- | --- | --- |
| Library of pure functions without DOM API calls | unit, integration | Node.js |
| Library with DOM API calls | unit, integration | [browsers](browsers.md) |
| Front-end component | unit, integration, functional | [browsers](browsers.md) |
| Application | unit, integration, functional | [browsers](browsers.md) |

## Set up Unit Tests in Sauce Labs

You can set up tests locally or on a CI server (Travis CI and the like). We will cover both cases here. Start with a setup [example](https://github.com/axemclion/grunt-saucelabs/tree/master/examples) for your testing framework and follow the steps to tweak an example.

#### 1. Prepare unit tests for the browsers

Depends on a [testing framework](https://mochajs.org/#running-mocha-in-the-browser).

#### 2. Set up test result reporting

Sauce Labs Selenium script needs a way to detect test results. Because tests can run asynchronously, it is not enough to wait for the `onload` event. Results are instead detected by polling a global variable on a page, which you will [need to provide](https://wiki.saucelabs.com/display/DOCS/Setting+Up+the+Reporting+Code+for+Your+JavaScript+Unit+Tests).

Variable name and value depends on a testing framework. Please consult the respective reporting [example](https://github.com/saucelabs-sample-scripts/JavaScript) for a particular framework. You can also use [our reporting script](https://github.com/vitalyq/react-trigger-change/blob/master/test/vendor/saucelabs-reporting.js) for Mocha:
```js
saucelabsReporting(mocha.run());
```

#### 3. Set up HTTP server

`grunt-saucelabs` examples suggest `grunt-contrib-connect` but any static server will work.

#### 4. Set up Sauce Connect

Sauce Connect is used to access your locally hosted tests from the Sauce Labs browsers.

`grunt-saucelabs` provides Sauce Connect from the `sauce-tunnel` module, but it's version was outdated at the time of writing and **IE9** tests were failing with it. If you are using `grunt-saucelabs`, we recommend disabling it's built-in Sauce Connect in `Gruntfile.js`:
```js
'saucelabs-mocha': {
  all: {
    options: {
      // ...
      tunneled: false
    }
  }
}
```

##### 4.1. Set up Sauce Connect locally

- [Download](https://wiki.saucelabs.com/display/DOCS/Sauce+Connect+Proxy) the executable
- Run `sc -u YOUR_USERNAME -k YOUR_ACCESS_KEY`

##### 4.2. Set up Sauce Connect with [Travis CI](https://docs.travis-ci.com/user/sauce-connect/)

We store credentials with [JWT addon](https://docs.travis-ci.com/user/jwt) to enable builds on pull requests.

- `gem install travis`
- Update `.travis.yml`:
```YAML
addons:
  sauce_connect:
    username: "Your Sauce Labs username"
  jwt:
    secure: "The secure string output by `travis encrypt SAUCE_ACCESS_KEY=Your Sauce Labs access key`"
```
- Update `Gruntfile.js` to use a tunnel provided by `sauce_connect` addon:
```js
'saucelabs-mocha': {
  all: {
    options: {
      // ...
      sauceConfig: {
        // ...
        tunnelIdentifier: process.env.TRAVIS_JOB_NUMBER
      },
      tunneled: false
    }
  }
}
```

#### 5. Run the tests

Sauce Labs provides high-level [API](https://wiki.saucelabs.com/display/DOCS/JavaScript+Unit+Testing+Methods) for running JavaScript unit tests. Thus, you don't need to set up Selenium or write a Selenium script to poll test results.

There is also [grunt-saucelabs](https://github.com/axemclion/grunt-saucelabs) task which wraps the API. It works by running `js-tests` method and then polling test results with `js-tests/status`. If any test fails, it will return a non-zero exit code. This is handy for a build process integration.
