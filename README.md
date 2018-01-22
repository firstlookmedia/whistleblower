# Whistleblower

Headless browser testing utils via [Jest](https://facebook.github.io/jest/) and
[Puppeteer](https://github.com/GoogleChrome/puppeteer), based on [Jest's
example integration](https://facebook.github.io/jest/docs/en/puppeteer.html).

## Usage

Install with `npm install firstlookmedia/whistleblower` or `yarn add
firstlookmedia/whistleblower`.

Create a [jest.config.js
file](https://facebook.github.io/jest/docs/en/configuration.html) that points to
Whistleblower's utils:
```javascript
module.exports = {
  globalSetup: 'whistleblower/setup',
  globalTeardown: 'whistleblower/teardown',
  testEnvironment: 'whistleblower/environment',
};
```

To run tests from the command line:
1. Supply the process with a hostname where your tests will run.
2. Use Whistleblower's installation of Jest (using a top-level or global Jest
   install can cause [problems when other Jest versions are
   present](https://stackoverflow.com/questions/43837596/projects-map-is-not-a-function-for-jest-cli)).
3. Pass Jest the path of your config file, along with any other [Jest
   options](https://facebook.github.io/jest/docs/en/cli.html).

For example:
```bash
HOSTNAME=www.example.com ./node_modules/whistleblower/node_modules/.bin/jest --config=path/to/your/jest.config.js
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
