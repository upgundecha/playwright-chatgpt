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

## Parameterizing test using CSV file

Here is an example of using a CSV file to parameterize tests in JavaScript using Playwright and the Mocha testing framework:

```javascript
const { expect } = require('chai')
const fs = require('fs')
const parse = require('csv-parse/lib/sync')
const { playwright } = require('playwright')

describe('my tests', () => {
  // Read the CSV file and parse the data into an array of objects
  const data = parse(fs.readFileSync('data.csv'), { columns: true })

  // Loop through each row of data in the CSV file
  data.forEach(row => {
    // Define a test for each row of data
    it(`should do something with ${row.input}`, async () => {
      // Launch a browser instance
      const browser = await playwright.chromium.launch()

      // Create a new context (i.e. a new incognito window)
      const context = await browser.newContext()

      // Create a new page
      const page = await context.newPage()

      // Navigate to a website that requires input
      await page.goto('https://www.example.com/')

      // Use the input value from the CSV file to fill in a form on the website
      await page.type('#input-field', row.input)

      // Submit the form
      await page.click('#submit-button')

      // Use the expected value from the CSV file to assert the result
      expect(await page.evaluate(() => document.querySelector('#result').textContent)).to.equal(row.expected)

      // Close the browser instance
      await browser.close()
    })
  })
})
```

In this example, we use the `parse` function from the `csv-parse` library to read a CSV file and parse the data into an array of objects. We then loop through each row of data in the file and define a test for each one. In the test, we use Playwright to launch a browser instance, navigate to a website that requires input, and fill in a form on the website using the input value from the CSV file. We then use the expected value from the CSV file to assert the result. This allows us to easily parameterize our tests using data from a CSV file, and automate the process of filling in forms and asserting the results using Playwright.

## Parameterizing test using JSON file

Here is an example of using a JSON file to parameterize tests in JavaScript using Playwright and the Mocha testing framework, along with an example JSON file:

```javascript
// tests.js
const { expect } = require('chai')
const fs = require('fs')
const { playwright } = require('playwright')

describe('my tests', () => {
  // Read the JSON file and parse the data into an array of objects
  const data = JSON.parse(fs.readFileSync('data.json', 'utf8'))

  // Loop through each object in the array
  data.forEach(obj => {
    // Define a test for each object
    it(`should do something with ${obj.input}`, async () => {
      // Launch a browser instance
      const browser = await playwright.chromium.launch()

      // Create a new context (i.e. a new incognito window)
      const context = await browser.newContext()

      // Create a new page
      const page = await context.newPage()

      // Navigate to a website that requires input
      await page.goto('https://www.example.com/')

      // Use the input value from the JSON file to fill in a form on the website
      await page.type('#input-field', obj.input)

      // Submit the form
      await page.click('#submit-button')

      // Use the expected value from the JSON file to assert the result
      expect(await page.evaluate(() => document.querySelector('#result').textContent)).to.equal(obj.expected)

      // Close the browser instance
      await browser.close()
    })
  })
})
```

The JSON file

```json
// data.json
[  {    "input": "hello",    "expected": "hello world"  },  {    "input": "goodbye",    "expected": "goodbye world"  }]
```

In this example, we use the `JSON.parse` method to read a JSON file and parse the data into an array of objects. We then loop through each object in the array and define a test for each one. In the test, we use Playwright to launch a browser instance, navigate to a website that requires input, and fill in a form on the website using the input value from the JSON file. We then use the expected value from the JSON file to assert the result. This allows us to easily parameterize our tests using data from a JSON file, and automate the process of filling in forms and asserting the results using Playwright.

The JSON file in this example contains two objects, each with an `input` and an `expected` field. These fields are used to provide the input and expected output for the tests. When the tests are run, they will be executed once for each object in the JSON file, using the `input` and `expected` values from that object.

## Parameterizing test using YAML file

Here is an example of using a YAML file to parameterize tests in JavaScript using Playwright and the Mocha testing framework, along with an example YAML file:

```javascript
// tests.js
const { expect } = require('chai')
const fs = require('fs')
const yaml = require('js-yaml')
const { playwright } = require('playwright')

describe('my tests', () => {
  // Read the YAML file and parse the data into an array of objects
  const data = yaml.safeLoad(fs.readFileSync('data.yaml', 'utf8'))

  // Loop through each object in the array
  data.forEach(obj => {
    // Define a test for each object
    it(`should do something with ${obj.input}`, async () => {
      // Launch a browser instance
      const browser = await playwright.chromium.launch()

      // Create a new context (i.e. a new incognito window)
      const context = await browser.newContext()

      // Create a new page
      const page = await context.newPage()

      // Navigate to a website that requires input
      await page.goto('https://www.example.com/')

      // Use the input value from the YAML file to fill in a form on the website
      await page.type('#input-field', obj.input)

      // Submit the form
      await page.click('#submit-button')

      // Use the expected value from the YAML file to assert the result
      expect(await page.evaluate(() => document.querySelector('#result').textContent)).to.equal(obj.expected)

      // Close the browser instance
      await browser.close()
    })
  })
})
```

The YAML file

```yaml
# data.yaml
- input: hello
  expected: hello world
- input: goodbye
  expected: goodbye world
```

In this example, we use the `yaml.safeLoad` method to read a YAML file and parse the data into an array of objects. We then loop through each object in the array and define a test for each one. In the test, we use Playwright to launch a browser instance, navigate to a website that requires input, and fill in a form on the website using the input value from the YAML file. We then use the expected value from the YAML file to assert the result. This allows us to easily parameterize our tests using data from a YAML file, and automate the process of filling in forms and asserting the results using Playwright.

The YAML file in this example contains two objects, each with an `input` and an `expected` field. These fields are used to provide the `input` and `expected` output for the tests. When the tests are run, they will be executed once for each object in the YAML file, using the `input` and `expected` values from that object.

### Using multiple test data

Here is an example of using a YAML file to parameterize tests in JavaScript using Playwright and the Mocha testing framework, along with an example YAML file containing multiple sets of test data:

```javascript
// tests.js
const { expect } = require('chai')
const fs = require('fs')
const yaml = require('js-yaml')
const { playwright } = require('playwright')

describe('my tests', () => {
  // Read the YAML file and parse the data into an array of objects
  const data = yaml.safeLoad(fs.readFileSync('data.yaml', 'utf8'))

  // Loop through each set of test data
  data.forEach(testData => {
    // Define a test for each set of data
    it(`should do something with ${testData.input}`, async () => {
      // Launch a browser instance
      const browser = await playwright.chromium.launch()

      // Create a new context (i.e. a new incognito window)
      const context = await browser.newContext()

      // Create a new page
      const page = await context.newPage()

      // Navigate to a website that requires input
      await page.goto('https://www.example.com/')

      // Use the input value from the YAML file to fill in a form on the website
      await page.type('#input-field', testData.input)

      // Submit the form
      await page.click('#submit-button')

      // Use the expected value from the YAML file to assert the result
      expect(await page.evaluate(() => document.querySelector('#result').textContent)).to.equal(testData.expected)

      // Close the browser instance
      await browser.close()
    })
  })
})
```
The YAML file
```yaml
# data.yaml
- input: hello
  expected: hello world
- input: goodbye
  expected: goodbye world
- input: foo
  expected: foo bar
- input: bar
  expected: bar baz
```

In this example, we use the `yaml.safeLoad` method to read a YAML file and parse the data into an array of objects. We then loop through each object in the array and define a test for each one. In the test, we use Playwright to launch a browser instance, navigate to a website that requires input, and fill in a form on the website using the input value from the YAML file. We then use the expected value from the YAML file to assert the result. This allows us to easily parameterize our tests using data from a YAML file, and automate the process of filling in forms and asserting the results using Playwright.
