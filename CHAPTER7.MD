# Chapter 7 - Parameterized Tests

To parameterize test in Playwright, you can use the `playwright.each` method, which allows you to define a set of test data and run the same test multiple times with different data values. This can be useful for testing different scenarios or conditions, or for verifying that your code is working properly with a variety of input values.

Here is an example that shows how to use the `playwright.each` method to use multiple test data in Playwright:

```javascript
const playwright = require('playwright');

const data = [
  { input: 'foo', expected: 'FOO' },
  { input: 'bar', expected: 'BAR' },
  { input: 'baz', expected: 'BAZ' },
];

describe('My test', () => {
  playwright.each(data).it('should convert $input to $expected', async ({ input, expected }) => {
    // Start a new browser instance
    const browser = await playwright.chromium.launch();

    // Create a new page
    const page = await browser.newPage();

    // Navigate to a web page
    await page.goto('https://example.com');

    // Enter the input value in the text field
    await page.type('#input', input);

    // Click the submit button
    await page.click('#submit');

    // Get the output value from the page
    const output = await page.evaluate(() => {
      return document.querySelector('#output').innerText;
    });

    // Verify that the output value is as expected
    expect(output).toEqual(expected);

    // Close the browser
    await browser.close();
  });
});
```
In this example, the `playwright.each` method is used to define a set of test data, with each data value containing an input and an expected value. The describe and it functions from the Jest testing framework are then used to define the test, and the `playwright.each` method is used.

Here is another example for testing different scenarios or configurations, or for running the same test on different browsers or devices:

```javascript
const playwright = require('playwright');

const parameters = [
  { name: 'Chrome', browser: 'chromium' },
  { name: 'Firefox', browser: 'firefox' },
  { name: 'Safari', browser: 'webkit' },
];

describe('My test', () => {
  playwright.each(parameters).it('should run on $name', async ({ browser }) => {
    // Start a new browser instance
    const b = await playwright[browser].launch();

    // Create a new page
    const page = await b.newPage();

    // Navigate to a web page
    await page.goto('https://example.com');

    // Perform some actions on the page

    // Close the browser
    await b.close();
  });
});
```
In this example, the `playwright.each` method is used to define a set of parameters for the test, with each parameter containing a `name` and a `browser` value. The describe and it functions from the Jest testing framework are then used to define the test, and the `playwright.each` method is used to run the test multiple times with different parameter values.

In the test body, the `browser` parameter is used to specify which browser to use for the test. The `playwright[browser].launch` method is used to start a new browser instance, and the `b.newPage` method is used to create a new page. The `page.goto` method is then used to navigate to a web page, and the test performs some actions on the page. Finally, the `b.close` method is used to close the browser instance and clean up any resources.



