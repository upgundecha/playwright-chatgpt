# Chapter 4 - Element Interaction

> **Note** 
> Plagiarism detected by Grammerly - 10%

## How does Playwright interact with the web application?

Playwright is a low-level library for automating web browsers, so it does not interact directly with your web application. Instead, it uses the web browser's APIs to control the browser and interact with the web page.

For example, if you want to fill out a form on a web page using Playwright, you would use the browser's fill method to enter the form data into the appropriate fields. Playwright would then use the browser's APIs to send the data to the web page and submit the form. The web application would then receive the data and process it as usual.

In this way, Playwright acts as a middleman between your tests and the web application. It allows you to automate the browser and interact with the web page, without needing to worry about the details of how the web application works or how it processes the data. This makes it easier to write reliable and maintainable tests for your web application.

## The `page` object in Playwright

In Playwright, the `page` object represents a web page in a browser, and provides various methods that you can use to interact with the page and its content. Some examples of page methods in Playwright include:

- `page.click`: This method simulates a mouse click on a given element on the page.
- `page.fill`: This method fills a form field on the page with a given value.
- `page.focus`: This method focuses a given element on the page, so that it can be interacted with.
- `page.goto`: This method navigates the page to a given URL.
- `page.hover`: This method simulates a mouse hover over a given element on the page.
- `page.screenshot`: This method takes a screenshot of the page and saves it to a file.
- `page.type`: This method simulates typing into a given element on the page.
- `page.waitForSelector`: This method waits for a given element to appear on the page, before continuing with the script.
- `page.$`: This method returns the first element on the page that matches a given CSS selector.

These are just a few examples of page methods in Playwright. There are many other methods available, which you can use to perform various actions on the page, such as interacting with elements, extracting information from the page, and more.

Overall, the page object in Playwright provide a powerful set of tools for automating and testing web pages, and are an essential part of the Playwright API.

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

#### The `fill` method

The process of filling a textbox in Playwright is similar to typing a value into a textbox, as shown in the previous example. Here is an example of how you could use Playwright to fill a textbox with a specific value:

```javascript
// Find the input textbox on the page
const input = await page.$('input[type="text"]');

// Fill the textbox with the desired value
await input.fill('Hello, world!');
```

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

## Get attribute value of an element

To get the value of an attribute for an element in Playwright, you can use the `element.getAttribute` method, as shown in the following example:

```javascript
const playwright = require('playwright');

(async () => {
  // Start a new browser instance
  const browser = await playwright.chromium.launch();

  // Create a new page
  const page = await browser.newPage();

  // Navigate to a web page
  await page.goto('https://example.com');

  // Find the element on the page
  const element = await page.$('#some-element');

  // Get the value of the "id" attribute for the element
  const id = await element.getAttribute('id');

  // Print the value of the "id" attribute to the console
  console.log(id);

  // Close the browser
  await browser.close();
})();
```
The `element.getAttribute` method is used to get the value of the "id" attribute for the element. This method returns a promise that resolves with the value of the attribute, or `null` if the attribute is not set for the element.

## Get CSS property of an element

To get the value of a CSS property for an element in Playwright, you can use the `element.getStyleProperty` method, as shown in the following example:

```javascript
const playwright = require('playwright');

(async () => {
  // Start a new browser instance
  const browser = await playwright.chromium.launch();

  // Create a new page
  const page = await browser.newPage();

  // Navigate to a web page
  await page.goto('https://example.com');

  // Find the element on the page
  const element = await page.$('#some-element');

  // Get the value of the "display" CSS property for the element
  const display = await element.getStyleProperty('display');

  // Print the value of the "display" property to the console
  console.log(display);

  // Close the browser
  await browser.close();
})();
```

The `element.getStyleProperty` method is used to get the value of the "display" CSS property for the element. This method returns a promise that resolves with the value of the property, or `null` if the property is not set for the element.

## Working with Select element

### Getting options from the Select element

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


### Selecting an option from the Select element

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


### Getting selected item from the Select element

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

## Working with Checkbox input element

Here is an example of how you could use Playwright to select and unselect a checkbox on a web page:

```javascript
const playwright = require('playwright');

(async () => {
  // Start a new browser instance
  const browser = await playwright.chromium.launch();

  // Create a new page
  const page = await browser.newPage();

  // Navigate to a web page
  await page.goto('https://example.com');

  // Find the checkbox on the page
  const checkbox = await page.$('input[type="checkbox"]');

  // Check if the checkbox is currently selected
  const isChecked = await checkbox.getAttribute('checked');

  // Select or unselect the checkbox, depending on its current state
  if (isChecked) {
    await checkbox.uncheck();
  } else {
    await checkbox.check();
  }

  // Wait for the page to update
  await page.waitForSelector('#selected-items', { visible: true });

  // Close the browser
  await browser.close();
})();
```

In this example, the `playwright.chromium.launch` method is used to start a new browser instance, and the `browser.newPage` method is used to create a new page. The `page.goto` method is then used to navigate to a web page, and the `page.$` method is used to find the input element on the page (i.e. the checkbox).

Note that the input element in this example has a `type` attribute set to "checkbox", which indicates that it is a checkbox. This is necessary because the `check` and `uncheck` methods can only be used with checkbox elements.

Once the checkbox is found, the `checkbox.getAttribute` method is used to get the current value of the "checked" attribute. This attribute is set to "true" if the checkbox is selected, or "false" if it is unselected.

The `if` statement then checks the value of the "checked" attribute, and either selects or unselects

## Working with Radio button input element

Here is an example of how you could use Playwright to select a radio button on a web page:

```javascript
const playwright = require('playwright');

(async () => {
  // Start a new browser instance
  const browser = await playwright.chromium.launch();

  // Create a new page
  const page = await browser.newPage();

  // Navigate to a web page
  await page.goto('https://example.com');

  // Find the radio button on the page
  const radioButton = await page.$('input[type="radio"][value="option1"]');

  // Check if the radio button is currently selected
  const isChecked = await radioButton.getAttribute('checked');

  // Select the radio button, if it is not already selected
  if (!isChecked) {
    await radioButton.click();
  }

  // Wait for the page to update
  await page.waitForSelector('#selected-option', { visible: true });

  // Close the browser
  await browser.close();
})();
```

The input element in this example has a `type` attribute set to "radio" and a `value` attribute set to "option1". This is necessary because the click method can only be used with radio buttons that have a specific value.

Once the radio button is found, the `radioButton.getAttribute` method is used to get the current value of the "checked" attribute. This attribute is set to "true" if the radio button is selected, or "false" if it is unselected.

The `if` statement then checks the value of the "checked" attribute, and only selects the radio button if

## Inspecting element state

### Element is visible

Here is an example of how you could use Playwright to check if an element is visible on a web page:

```javascript
const playwright = require('playwright');

(async () => {
  // Start a new browser instance
  const browser = await playwright.chromium.launch();

  // Create a new page
  const page = await browser.newPage();

  // Navigate to a web page
  await page.goto('https://example.com');

  // Find the element on the page
  const element = await page.$('#some-element');

  // Check if the element is visible
  const isVisible = await element.isIntersectingViewport();

  // Print the result to the console
  console.log(isVisible);

  // Close the browser
  await browser.close();
})();
```
The `element.isIntersectingViewport` method is used to check if the element is visible. This method returns `true` if the element is visible, or `false` if it is not visible (e.g. because it is hidden, or because it is outside the viewport).

The result of the `isIntersectingViewport` method is then printed to the console using the `console.log` method, so that you can see if the element is visible or not.

There is another method using the "display" CSS property for the element.

```javascript
// Find the element on the page
const element = await page.$('#some-element');

// Check if the element is displayed
const isDisplayed = await element.getStyleProperty('display') !== 'none';

// Print the result to the console
console.log(isDisplayed);
```

The `element.getStyleProperty` method is used to get the value of the "display" CSS property for the element. This property determines whether or not the element is displayed on the page.

If the "display" property is set to "none", it means that the element is not displayed on the page, and the `isDisplayed` variable is set to `false`. Otherwise, the `isDisplayed` variable is set to `true`, indicating that the element is displayed on the page.

### Element is enabled

Here is an example of how you could use Playwright to check if an element is enabled on a web page:

```javascript
const playwright = require('playwright');

(async () => {
  // Start a new browser instance
  const browser = await playwright.chromium.launch();

  // Create a new page
  const page = await browser.newPage();

  // Navigate to a web page
  await page.goto('https://example.com');

  // Find the element on the page
  const element = await page.$('#some-element');

  // Check if the element is enabled
  const isEnabled = await element.getAttribute('disabled') !== 'true';

  // Print the result to the console
  console.log(isEnabled);

  // Close the browser
  await browser.close();
})();
```

The `element.getAttribute` method is used to get the value of the "disabled" attribute for the element. This attribute determines whether or not the element is enabled on the page.

If the "disabled" attribute is set to "true", it means that the element is not enabled on the page, and the `isEnabled` variable is set to `false`. Otherwise, the `isEnabled` variable is set to `true`, indicating that the element is enabled on the page.

## Taking Screenshot of an element

To take a screenshot of a specific element on a web page using Playwright, you can use the `element.screenshot` method, as shown in the following example:

```javascript
const playwright = require('playwright');

(async () => {
  // Start a new browser instance
  const browser = await playwright.chromium.launch();

  // Create a new page
  const page = await browser.newPage();

  // Navigate to a web page
  await page.goto('https://example.com');

  // Find the element on the page
  const element = await page.$('#some-element');

  // Take a screenshot of the element and save it to a file
  await element.screenshot({ path: 'element-screenshot.png' });

  // Close the browser
  await browser.close();
})();
```
Once the element is found, the `element.screenshot` method is used to take a screenshot of the element and save it to a file. This method takes an options object as an argument, which can be used to specify the `path` where the screenshot should be saved. The screenshot is then saved to the specified file using the `path` option, 

## Getting Size and Location of an element

To get the size and location of an element on a web page using Playwright, you can use the `element.boundingBox` method, as shown in the following example:

```javascript
const playwright = require('playwright');

(async () => {
  // Start a new browser instance
  const browser = await playwright.chromium.launch();

  // Create a new page
  const page = await browser.newPage();

  // Navigate to a web page
  await page.goto('https://example.com');

  // Find the element on the page
  const element = await page.$('#some-element');

  // Get the size and location of the element
  const { x, y, width, height } = await element.boundingBox();

  // Print the size and location of the element to the console
  console.log(`Element is located at x=${x}, y=${y}, and has a width of ${width} and a height of ${height}.`);

  // Close the browser
  await browser.close();
})();
```

The `element.boundingBox method` is used to get the size and location of the element. This method returns an object with the properties `x`, `y`, `width`, and `height`, which represent the coordinates of the top-left corner of the element, as well as the element's width and height, respectively.

## Working with the Canvas element

To interact with a canvas element on a web page using Playwright, you can use the `page.$eval` method, which allows you to evaluate JavaScript code in the context of the page and interact with the canvas element.

Here is an example that shows how to use the `page.$eval` method to interact with a canvas element on a web page:

```javascript
const playwright = require('playwright');

(async () => {
  // Start a new browser instance
  const browser = await playwright.chromium.launch();

  // Create a new page
  const page = await browser.newPage();

  // Navigate to a web page with a canvas element
  await page.goto('https://example.com/canvas');

  // Find the canvas element on the page
  const canvas = await page.$('#my-canvas');

  // Use the $eval method to interact with the canvas element
  await canvas.$eval('#my-canvas', (canvas) => {
    // Get the canvas context
    const ctx = canvas.getContext('2d');

    // Draw a circle on the canvas
    ctx.beginPath();
    ctx.arc(100, 100, 50, 0, 2 * Math.PI);
    ctx.fill();
  });

  // Close the browser
  await browser.close();
})();
```

In this example, the `playwright.chromium.launch` method is used to start a new browser instance, and the `browser.newPage` method is used to create a new page. The `page.goto` method is then used to navigate to a web page with a canvas element, and the `page.$` method is used to find the canvas element on the page.

Once the canvas element is found, the `canvas.$eval` method is used to evaluate JavaScript code in the context of the page and interact with the canvas element. In this case, the code uses the `canvas.getContext` method to get the canvas context, and then uses the context to draw a circle on the canvas.

Overall, this code shows how you can use Playwright to interact with a canvas element on a web page and perform actions such as drawing or animating on the canvas. You can use similar approaches to interact with other elements or components on the page, such as images, videos, or interactive forms.

## Working with the SVG element

To work with SVG elements in Playwright, you can use the `page.$eval` or `page.evaluate` method to query the SVG elements using CSS selectors, and then use the methods provided by Playwright to interact with the elements.

Here is an example of how to use Playwright to click on an SVG element:

```javascript
const browser = await playwright.chromium.launch()
const context = await browser.newContext()
const page = await context.newPage()

await page.goto('https://www.example.com/')

// Query the SVG element using a CSS selector
const svgElement = await page.$eval('#my-svg-element', el => el)

// Use the click method provided by Playwright to click on the element
await svgElement.click()
```

In this example, we use the `page.$eval` method to query the SVG element using a CSS selector, and then use the `click` method provided by Playwright to click on the element. This allows us to easily interact with SVG elements using Playwright.

Note that some methods, such as `click`, are not available for all types of elements. In such cases, you can use the `page.evaluate` method to execute JavaScript code that interacts with the SVG elements directly. For example:

```javascript
const browser = await playwright.chromium.launch()
const context = await browser.newContext()
const page = await context.newPage()

await page.goto('https://www.example.com/')

// Query the SVG element using a CSS selector
const svgElement = await page.$eval('#my-svg-element', el => el)

// Use the page.evaluate method to execute JavaScript code that clicks on the element
await page.evaluate(svgElement => svgElement.click(), svgElement)
```

In this example, we use the `page.evaluate` method to execute JavaScript code that clicks on the SVG element. This allows us to interact with the SVG element even if the Playwright API does not provide a method for the desired action.
