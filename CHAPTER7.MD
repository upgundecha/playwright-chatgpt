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


## Generating test data using Faker

Faker is a library for generating fake data. It can be used to generate things like fake names, addresses, emails, and more. This fake data can be useful for testing purposes, for example, when you want to test how your code handles different inputs without using real data.

Playwright is a library for automating browser interactions. It can be used to automate tasks like filling in forms, clicking buttons, and more.

Faker can be used with Playwright to automatically generate fake data and use it to fill in forms on websites. This can be useful for testing purposes, as it allows you to quickly and easily test how your code handles different inputs without having to manually enter the data each time. For example, you could use Faker to generate a fake email address, and then use Playwright to automatically fill in a form on a website with that email address. This would save you time and effort, and allow you to quickly test your code with different inputs.

Here is an example of using Faker with Playwright:

```javascript
const { Faker } = require('faker')
const { playwright } = require('playwright')

const faker = new Faker()

async function main() {
  // Launch a browser instance
  const browser = await playwright.chromium.launch()

  // Create a new context (i.e. a new incognito window)
  const context = await browser.newContext()

  // Create a new page
  const page = await context.newPage()

  // Generate a fake email address
  const email = faker.internet.email()

  // Navigate to a website that asks for your email
  await page.goto('https://www.example.com/')

  // Type the email address into the email field on the website
  await page.type('#email-field', email)

  // Submit the form
  await page.click('#submit-button')

  // Close the browser instance
  await browser.close()
}

main()

```

In this example, we use Faker to generate a fake email address, which we then use to fill in a form on a website using Playwright. This could be useful for testing purposes, for example.
