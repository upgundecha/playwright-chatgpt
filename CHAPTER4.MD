# Chapter 4 - Element Interaction

## How does Playwright interact with the web application?

Playwright is a low-level library for automating web browsers, so it does not interact directly with your web application. Instead, it uses the web browser's APIs to control the browser and interact with the web page.

For example, if you want to fill out a form on a web page using Playwright, you would use the browser's fill method to enter the form data into the appropriate fields. Playwright would then use the browser's APIs to send the data to the web page and submit the form. The web application would then receive the data and process it as usual.

In this way, Playwright acts as a middleman between your tests and the web application. It allows you to automate the browser and interact with the web page, without needing to worry about the details of how the web application works or how it processes the data. This makes it easier to write reliable and maintainable tests for your web application.

## Performing click action on element

Here is an example of how you could use Playwright to click on a button on a web page:

```javascript
const playwright = require('playwright');

(async () => {
  // Start a new browser instance
  const browser = await playwright.chromium.launch();

  // Create a new page
  const page = await browser.newPage();

  // Navigate to a web page
  await page.goto('https://example.com');

  // Find the button element on the page
  const button = await page.$('button[type="submit"]');

  // Click on the button
  await button.click();

  // Wait for the page to load
  await page.waitForNavigation();

  // Close the browser
  await browser.close();
})();
```

In this example, the `playwright.chromium.launch` method is used to start a new browser instance, and the `browser.newPage` method is used to create a new page. The `page.goto` method is then used to navigate to a web page, and the `page.$` method is used to find the button element on the page.

Once the button is found, the `button.click` method is used to click on it. This will simulate a user clicking on the button with their mouse, and will trigger any associated events or actions in the web page.

After clicking on the button, the `page.waitForNavigation` method is used to wait for the page to finish loading. This is important because clicking on the button may cause the page to navigate to a new URL, and you need to wait for the navigation to complete before continuing.

Finally, the `browser.close` method is used to close the browser instance and clean up any resources.

Overall, this code shows how you can use Playwright to find and interact with elements on a web page, such as clicking on a button. You can use similar approaches

## Working with input textbox element

### Typing a value in a input textbox element

Here is an example of how you could use Playwright to type a value into an input textbox on a web page:

```javascript
const playwright = require('playwright');

(async () => {
  // Start a new browser instance
  const browser = await playwright.chromium.launch();

  // Create a new page
  const page = await browser.newPage();

  // Navigate to a web page
  await page.goto('https://example.com');

  // Find the input textbox on the page
  const input = await page.$('input[type="text"]');

  // Type the desired value into the textbox
  await input.type('Hello, world!');

  // Wait for the page to update
  await page.waitForSelector('#typed-text', { visible: true });

  // Close the browser
  await browser.close();
})();
```

The `input.type` method is used to type the desired value into the textbox. This method simulates a user typing on a keyboard, and will trigger any associated events or actions in the web page.

### Getting value from the input textbox

Here is an example of how you could use Playwright to get the value of an input textbox on a web page:

```javascript

// Find the input textbox on the page
const input = await page.$('input[type="text"]');

// Get the value of the input textbox
const value = await input.getValue();

// Print the value to the console
console.log(value);
```

The `input.getValue` method is used to get the current value of the textbox. This method will return the value of the textbox, or an empty string if the textbox is empty.

## Working with Dropdown element

### Getting options from the Dropdown element

Here is an example of how you could use Playwright to get all the options from a dropdown menu on a web page:

```javascript
const playwright = require('playwright');

(async () => {
  // Start a new browser instance
  const browser = await playwright.chromium.launch();

  // Create a new page
  const page = await browser.newPage();

  // Navigate to a web page
  await page.goto('https://example.com');

  // Find the dropdown menu on the page
  const dropdown = await page.$('select');

  // Get the options from the dropdown
  const options = await dropdown.$$eval('option', (options) => options.map((option) => option.value));

  // Print the options to the console
  console.log(options);

  // Close the browser
  await browser.close();
})();
```

The `dropdown.$$eval` method is used to evaluate a JavaScript function that finds all the `option` elements inside the dropdown menu. The function then returns an array of the values of the `option` elements, which is stored in the `options` variable.

The options are then printed to the console using the `console.log` method. You can use this array in any way you want, such as verifying that it contains the expected options, or using it to perform further actions on the page.


### Selecting an option from the Dropdown element

Here is an example of how you could use Playwright to select an item from a dropdown menu on a web page:

```javascript
const playwright = require('playwright');

(async () => {
  // Start a new browser instance
  const browser = await playwright.chromium.launch();

  // Create a new page
  const page = await browser.newPage();

  // Navigate to a web page
  await page.goto('https://example.com');

  // Find the dropdown menu on the page
  const dropdown = await page.$('select');

  // Select the desired item from the dropdown
  await dropdown.selectOption('Option 2');

  // Wait for the page to update
  await page.waitForSelector('#selected-item', { visible: true });

  // Close the browser
  await browser.close();
})();
```

The `dropdown.selectOption` method is used to select the desired option from the menu. This will simulate a user clicking on the option with their mouse, and will trigger any associated events or actions in the web page.

#### Selecting multiple options in a multi-select Dropdown element

Here is an example of how you could use Playwright to select multiple items from a dropdown menu on a web page:

```javascript

// Find the dropdown menu on the page
const dropdown = await page.$('select[multiple]');

// Select the desired items from the dropdown
await dropdown.selectOption('Option 2');
await dropdown.selectOption('Option 4');

```
The `dropdown.selectOption` method is used to select the desired options from the menu. This method can be called multiple times to select multiple options.


### Getting selected item from the Dropdown element

Here is an example of how you could use Playwright to get the selected item from a dropdown menu on a web page:

```javascript
const playwright = require('playwright');

(async () => {
  // Start a new browser instance
  const browser = await playwright.chromium.launch();

  // Create a new page
  const page = await browser.newPage();

  // Navigate to a web page
  await page.goto('https://example.com');

  // Find the dropdown menu on the page
  const dropdown = await page.$('select');

  // Get the selected option from the dropdown
  const selectedOption = await dropdown.getValue();

  // Print the selected option to the console
  console.log(selectedOption);

  // Close the browser
  await browser.close();
})();
```

The `dropdown.getValue` method is used to get the currently selected option from the menu. This method will return the value of the selected option, or an empty string if no option is selected.
