# Set up Unit Tests in Sauce Labs

You can set up tests locally or on a CI server. We will cover both cases here. Start with a setup [example](https://github.com/axemclion/grunt-saucelabs/tree/master/examples) for your testing framework and follow the steps to tweak an example.

### 1. Prepare unit tests for the browsers

How you do that depends on a [testing framework](https://mochajs.org/#running-mocha-in-the-browser).

### 2. Set up test result reporting

Sauce Labs Selenium script needs a way to detect test results. Because tests can run asynchronously, it is not enough to wait for the `onload` event. Results are instead detected by polling a global variable on a page, which you will need to provide.

Variable name and value depend on a testing framework. Please consult a reporting script example in the `index.html` file. You need to implement the reporting for your test's `html` file. You can also use [our reporting script](https://github.com/vitalyq/react-trigger-change/blob/master/test/vendor/saucelabs-reporting.js) for Mocha:
```js
saucelabsReporting(mocha.run());
```

### 3. Prepare a script to execute the tests

Sauce Labs provides high-level REST API for running JavaScript unit tests. Thus, you don't need to set up Selenium or write a Selenium script to poll a test result variable on a page.

There is also [grunt-saucelabs](https://github.com/axemclion/grunt-saucelabs) task which wraps the API. It works by running `js-tests` API method and then polling test results on a server with `js-tests/status`. If any test fails, it will return a non-zero exit code. This is handy for integration with a build process.

To set up `grunt-saucelabs` run:
```
npm install grunt grunt-saucelabs grunt-contrib-connect --save-dev
```

Copy `Gruntfile.js` from the example. We recommend updating these fields:

```js
'saucelabs-mocha': {
  all: {
    options: {
      // ...
      urls: urls, // test URLs
      throttled: 5, // max current sessions
      sauceConfig: {
        // ...
        recordVideo: false,
        recordScreenshots: false
      }
    }
  }
}
```

- Update the `urls` property with an array of your test URLs
- Set `throttled` value to the `current sessions` maximum value on your Sauce Labs dashboard
- Disable video and screenshot recording by setting `sauceConfig.recordVideo` and `sauceConfig.recordScreenshots` to false

### 4. Set up HTTP server

`grunt-saucelabs` examples suggest `grunt-contrib-connect` but any static server will work.

### 5. Set up Sauce Connect

Sauce Connect is used to access your locally hosted tests from the Sauce Labs browsers.

`grunt-saucelabs` provides Sauce Connect from the `sauce-tunnel` module, but its version was outdated at the time of writing and **IE9** tests were failing with it. We recommend disabling a built-in Sauce Connect in `Gruntfile.js`:
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

#### 5.1. Set up Sauce Connect locally

- [Download](https://wiki.saucelabs.com/display/DOCS/Sauce+Connect+Proxy) the executable
- Run `sc -u YOUR_USERNAME -k YOUR_ACCESS_KEY`

#### 5.2. Set up Sauce Connect with [Travis CI](https://docs.travis-ci.com/user/sauce-connect/)

- Disable **Build pushed pull requests** in repository settings
- Add environment variables `SAUCE_USERNAME` and `SAUCE_ACCESS_KEY` with Sauce Labs credentials
- Update `.travis.yml`:
```YAML
addons:
  sauce_connect: true
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

### 6. Run the tests

If Sauce Connect is up and running, you are now ready to run the tests:

```
grunt
```
