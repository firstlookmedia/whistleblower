# Whistleblower

Headless browser testing utils via [Jest](https://facebook.github.io/jest/) and
[Puppeteer](https://github.com/GoogleChrome/puppeteer), based on [Jest's
example integration](https://facebook.github.io/jest/docs/en/puppeteer.html).

## Usage

Requires Node v7.6.0 or later (upgrade to latest stable version on command line with `n stable`).

Install with `npm install firstlookmedia/whistleblower` or `yarn add
firstlookmedia/whistleblower`.

Create a [Jest config
file](https://facebook.github.io/jest/docs/en/configuration.html) that points to
Whistleblower's utils. This may also include other Jest config options.
```javascript
module.exports = {
  globalSetup: 'whistleblower/setup',
  globalTeardown: 'whistleblower/teardown',
  testEnvironment: 'whistleblower/environment',
};
```

To run tests from the command line:
1. Supply the process with a `HOSTNAME` environment variable, where your tests
   will run.
2. Pass Whistleblower the path of your config file, along with any other [Jest
   CLI options](https://facebook.github.io/jest/docs/en/cli.html).

For example:
```bash
HOSTNAME=www.example.com ./node_modules/.bin/whistleblower --config=path/to/your/config.js
```

In your test files, access the hostname you provided and a Puppeteer browser
instance on the `global` object, e.g.:
```javascript
describe('Homepage', () => {
  test('returns 200', async () => {
    const page = await global.__BROWSER__.newPage();
    const response = await page.goto(`https://${global.__HOSTNAME__}`);
    expect(response.status).toBe(200);
  });
});
```

## Common Errors
```bash
Timeout - Async callback was not invoked within the 5000ms timeout specified by jest.setTimeout.
```
This is a frequent error that occurs when puppeteer takes too long to complete its procedures. Use the second argument in a `test` block to increase Jest's default timeout value of 5000ms as such:
```javascript
describe('Issue Page', () => {
  test('returns 200', async () => {
    const page = await global.__BROWSER__.newPage();
    const response = await page.goto(`https://${global.__HOSTNAME__}/${issue.speakingId}`);
    expect(response.status).toBe(200);
  }, 20000);
});
```
