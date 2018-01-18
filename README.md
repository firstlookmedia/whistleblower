# Whistleblower

Headless browser testing utils via [Jest](https://facebook.github.io/jest/) and
[Puppeteer](https://github.com/GoogleChrome/puppeteer), based on [Jest's
example integration](https://facebook.github.io/jest/docs/en/puppeteer.html).

## Usage

```bash
npm install jest maxnewlands/whistleblower
```
(Using Yarn to install Jest threw errors when I tried to run it, possibly due
to my having other Jest versions installed in `node_modules`.)

Point to Whistleblower's utils in your [jest.config.js
file](https://facebook.github.io/jest/docs/en/configuration.html):
```javascript
module.exports = {
  globalSetup: 'whistleblower/setup',
  globalTeardown: 'whistleblower/teardown',
  testEnvironment: 'whistleblower/environment',
};
```

To run tests, supply the process a `HOSTNAME` value against which your tests
will run, and point to your Jest config:
```bash
HOSTNAME=www.example.com ./node_modules/.bin/jest --config=path/to/your/jest.config.js
```

In your test files, access the hostname you provided and a Puppeteer browser
instance on the `global` object, e.g.:
```javascript
describe('Homepage', () => {
  it('returns 200', async () => {
    const page = await global.__BROWSER__.newPage();
    const response = await page.goto(`https://${global.__HOSTNAME__}`);
    expect(response.status).toBe(200);
  });
});
```
