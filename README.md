# Whistleblower

Headless browser testing utils via Jest and Puppeteer, based on [Jest's
example](https://facebook.github.io/jest/docs/en/puppeteer.html).

## Usage

```bash
yarn add jest
```

(TBD: install whistleblower)

Point to whistleblower's utils in your [jest.config.js
file](https://facebook.github.io/jest/docs/en/configuration.html):
```javascript
module.exports = {
  globalSetup: 'whistleblower/setup',
  globalTeardown: 'whistleblower/teardown',
  testEnvironment: 'whistleblower/environment',
};
```

To run tests, supply the process a `HOSTNAME` value, against which to run your
tests, and point to your Jest config:
```bash
HOSTNAME=www.yourdomain.com jest --config path/to/your/jest.config.js
```


