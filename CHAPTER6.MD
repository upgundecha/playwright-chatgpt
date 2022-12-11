# Chapter 6 - Interacting with Page

## Using the `page` object

In Playwright, the `page` object provides several methods for navigating within a web page or between multiple pages. These methods include:

- `page.click(selector)`: This method simulates a click on an element that matches the given CSS selector.
- `page.fill(selector, value)`: This method fills in a form field with the given value. The field is selected using a CSS selector.
- `page.goto(url)`: This method navigates the page to the specified URL.
- `page.keyboard.press(key, options): This method simulates a press of the specified key on the keyboard. The options argument can be used to specify modifier keys like Shift or Alt.
- `page.mouse.click(x, y, options)`: This method simulates a click at the specified coordinates on the page. The options argument can be used to specify modifier keys like Shift or Alt.
- `page.reload()`: This method reloads the current page.
- `page.screenshot(path)`: This method saves a screenshot of the current page to the specified file path.
- `page.selectOption(selector, value)`: This method selects an option from a dropdown menu. The menu is selected using a CSS selector, and the option is specified by its value.
- `page.type(selector, text)`: This method types the given text into a form field or other editable element. The element is selected using a CSS selector.

## Performing Browser Navigation

In Playwright, you can use the `page.goto` method to navigate to a new page, the `page.reload` method to reload the current page, and the `page.goBack` and `page.goForward` methods to navigate to the previous or next page in the browser's history, respectively.

Here is a simple example of how you might use these methods in Playwright to perform page navigation:

```javascript
const { playwright } = require('playwright');

(async () => {
  const browser = await playwright.chromium.launch();
  const context = await browser.newContext();
  const page = await context.newPage();

  // Navigate to a new page
  await page.goto('http://localhost:3000/home');

  // Reload the current page
  await page.reload();

  // Navigate to the previous page in the browser's history
  await page.goBack();

  // Navigate to the next page in the browser's history
  await page.goForward();

  await browser.close();
})();
```

## Handling Alerts

In Playwright, you can use the `page.on` method to handle alerts that are displayed by a web page. This can be useful if you want to automatically accept or dismiss an alert, or if you want to assert the alert's message or other properties.

Here is a simple example of how you might use the `page.on` method in Playwright to handle an alert:

```javascript
const { playwright } = require('playwright');

(async () => {
  const browser = await playwright.chromium.launch();
  const context = await browser.newContext();
  const page = await context.newPage();
  await page.goto('http://localhost:3000');

  // Handle the "beforeunload" event, which is triggered when the page is about to be unloaded
  page.on('dialog', async (dialog) => {
    // Assert the alert's message
    expect(dialog.message()).toBe('Are you sure you want to leave?');

    // Accept the alert
    await dialog.accept();
  });

  // Click a link that will trigger the "beforeunload" event
  await page.click('a.leave-page-link');

  // Wait for the page to navigate to the next page
  await page.waitForNavigation();

  // Assert that the correct page is displayed
  const url = await page.url();
  expect(url).toBe('http://localhost:3000/goodbye');

  await browser.close();
})();
```

In this example, the `page.on` method is used to register a handler for the dialog event, which is triggered when an alert is displayed by the page. The handler function receives a `dialog` object as its argument, which provides methods like `message` and `accept` for interacting with the alert. In this example, the alert's `message` is asserted, and the alert is accepted by calling the `accept` method.

The `dialog` object in Playwright provides several methods for interacting with an alert, confirm, or prompt dialog that is displayed by a web page. These methods include:

- `dialog.accept([promptText])`: This method accepts the dialog and returns a promise that resolves when the dialog has been accepted. If the dialog is a prompt dialog, you can pass a promptText argument to provide a value for the prompt.
- `dialog.dismiss([promptText])`: This method dismisses the dialog and returns a promise that resolves when the dialog has been dismissed. If the dialog is a prompt dialog, you can pass a promptText argument to provide a value for the prompt.
- `dialog.message()`: This method returns the message of the dialog as a string.
- `dialog.type()`: This method returns the type of the dialog, which can be alert, confirm, or prompt.

These are just a few examples of the methods that the dialog object provides in Playwright

## Using `waitFor`

In Playwright, you can use the `waitFor` method to pause your test script until a specific condition is met. This can be useful if you need to wait for an element to be displayed on the page, or for an asynchronous operation to complete before continuing with your test.

Here is a simple example of how you might use the `waitFor` method in Playwright:

```javascript
const { playwright } = require('playwright');

(async () => {
  const browser = await playwright.chromium.launch();
  const context = await browser.newContext();
  const page = await context.newPage();
  await page.goto('http://localhost:3000');

  // Wait for the "submit" button to be displayed on the page
  await page.waitFor('button.submit-button');

  // Click the "submit" button
  await page.click('button.submit-button');

  // Wait for the page to navigate to the next page
  await page.waitForNavigation();

  // Assert that the correct page is displayed
  const url = await page.url();
  expect(url).toBe('http://localhost:3000/welcome');

  await browser.close();
})();
```

In this example, the `waitFor` method is used twice: once to wait for the "submit" button to be displayed on the page, and once to wait for the page to navigate to a new URL after the button is clicked.

The `waitFor` method takes a CSS selector as its first argument, which specifies the element that you want to wait for. It also takes an optional second argument, which is an object that can contain options like a timeout or a polling interval. If the specified element is not found on the page within the specified timeout, the `waitFor` method will throw an error.

Here is an example of how you might specify a timeout for the waitFor method in Playwright:

```javascript
const { playwright } = require('playwright');

(async () => {
  const browser = await playwright.chromium.launch();
  const context = await browser.newContext();
  const page = await context.newPage();
  await page.goto('http://localhost:3000');

  // Wait for the "submit" button to be displayed on the page, with a timeout of 5 seconds
  await page.waitFor('button.submit-button', { timeout: 5000 });

  // Click the "submit" button
  await page.click('button.submit-button');

  // Wait for the page to navigate to the next page, with a timeout of 5 seconds
  await page.waitForNavigation({ timeout: 5000 });

  // Assert that the correct page is displayed
  const url = await page.url();
  expect(url).toBe('http://localhost:3000/welcome');

  await browser.close();
})();
```

In this example, the `waitFor` method is called with a second argument that specifies a timeout of 5 seconds. If the specified element is not found on the page within 5 seconds, the `waitFor` method will throw an error.

You can specify a different timeout for each call to the waitFor method, depending on your specific needs.

### Using the `waitForFunction`

In Playwright, you can use the `waitForFunction` method to pause your test script until a specific condition is met. This can be useful if you need to wait for a change in an element's attribute value or style, or for any other condition that cannot be checked using a simple CSS selector.

Here is a simple example of how you might use the `waitForFunction` method in Playwright:

```javascript
const { playwright } = require('playwright');

(async () => {
  const browser = await playwright.chromium.launch();
  const context = await browser.newContext();
  const page = await context.newPage();
  await page.goto('http://localhost:3000');

  // Wait for the "submit" button to have a "disabled" attribute with a value of "false"
  await page.waitForFunction(
    () => document.querySelector('button.submit-button').getAttribute('disabled') === 'false',
    { timeout: 5000 }
  );

  // Click the "submit" button
  await page.click('button.submit-button');

  // Wait for the "message" element to have a "display" style of "block"
  await page.waitForFunction(
    () => document.querySelector('div.message').style.display === 'block',
    { timeout: 5000 }
  );

  // Assert that the "message" element is displayed on the page
  const message = await page.$eval('div.message', (el) => el.innerText);
  expect(message).toBe('Thanks for submitting the form!');

  await browser.close();
})();
```

In this example, the `waitForFunction` method is used twice: once to wait for the "submit" button to have a "disabled" attribute with a value of "false", and once to wait for the "message" element to have a "display" style of "block".

The `waitForFunction` method takes a JavaScript function as its first argument, which specifies the condition that you want to wait for. The function should return a truthy value when the condition is met, and a falsy value otherwise. The `waitForFunction` method also takes an optional second argument, which is an object that can contain options like a timeout or a polling interval. If the specified condition is not met within the specified timeout, the `waitForFunction` method will throw an error.

## Testing the clipboard contents

To test clipboard contents in Playwright, you can use the `page.clipboard` property to access the clipboard and assert its contents using the expect function from the chai library.

Here is an example of how to test clipboard contents in Playwright:

```javascript
const { expect } = require('chai')
const { playwright } = require('playwright')

describe('my tests', () => {
  // Define a test for the clipboard
  it('should have the expected contents', async () => {
    // Launch a browser instance
    const browser = await playwright.chromium.launch()

    // Create a new context (i.e. a new incognito window)
    const context = await browser.newContext()

    // Create a new page
    const page = await context.newPage()

    // Set the clipboard contents
    await page.clipboard.write({ text: 'hello world' })

    // Use the expect function from the 'chai' library to assert the clipboard contents
    expect(await page.clipboard.read()).to.deep.equal({ text: 'hello world' })

    // Close the browser instance
    await browser.close()
  })
})
```
In this example, we use the `page.clipboard.write` method to set the clipboard contents, and the `page.clipboard.read` method to read the clipboard contents and assert them using the expect function from the chai library. This allows us to easily test the contents of the clipboard in Playwright.

## Testing geolocation

To test geolocation in Playwright, you can use the `page.setGeolocation` method to set the geolocation of the page, and then use the `page.evaluate` method to execute JavaScript code that retrieves and asserts the geolocation using the `navigator.geolocation` API.

Here is an example of how to test geolocation in Playwright:

```javascript
const { expect } = require('chai')
const { playwright } = require('playwright')

describe('my tests', () => {
  // Define a test for the geolocation
  it('should have the expected coordinates', async () => {
    // Launch a browser instance
    const browser = await playwright.chromium.launch()

    // Create a new context (i.e. a new incognito window)
    const context = await browser.newContext()

    // Create a new page
    const page = await context.newPage()

    // Set the geolocation of the page
    await page.setGeolocation({ latitude: 37.422, longitude: -122.084 })

    // Use the page.evaluate method to execute JavaScript code that retrieves and asserts the geolocation
    const coordinates = await page.evaluate(() => {
      // Use the 'navigator.geolocation' API to retrieve the current geolocation
      return new Promise((resolve, reject) => {
        navigator.geolocation.getCurrentPosition(
          position => resolve({
            latitude: position.coords.latitude,
            longitude: position.coords.longitude,
          }),
          error => reject(error)
        )
      })
    })

    // Use the expect function from the 'chai' library to assert the geolocation coordinates
    expect(coordinates).to.deep.equal({ latitude: 37.422, longitude: -122.084 })

    // Close the browser instance
    await browser.close()
  })
})
```

In this example, we use the `page.setGeolocation` method to set the geolocation of the page, and the `page.evaluate` method to execute JavaScript code that retrieves the geolocation using the `navigator.geolocation` API. We then use the expect function from the chai library to assert the geolocation coordinates. This allows us to easily test the geolocation of a page in Playwright.

## Testing cookies

To test cookies in Playwright, you can use the page.setCookie method to set cookies on a page, and the page.cookies property to retrieve and assert the cookies using the expect function from the chai library.

Here is an example of how to test cookies in Playwright:

```javascript
const { expect } = require('chai')
const { playwright } = require('playwright')

describe('my tests', () => {
  // Define a test for the cookies
  it('should have the expected contents', async () => {
    // Launch a browser instance
    const browser = await playwright.chromium.launch()

    // Create a new context (i.e. a new incognito window)
    const context = await browser.newContext()

    // Create a new page
    const page = await context.newPage()

    // Set a cookie on the page
    await page.setCookie({
      name: 'my-cookie',
      value: 'hello world',
    })

    // Use the page.cookies property to retrieve the cookies from the page
    const cookies = await page.cookies()

    // Use the expect function from the 'chai' library to assert the cookie contents
    expect(cookies).to.deep.include({
      name: 'my-cookie',
      value: 'hello world',
    })

    // Close the browser instance
    await browser.close()
  })
})
```

In this example, we use the `page.setCookie` method to set a cookie on the page, and the `page.cookies` property to retrieve the cookies from the page. We then use the expect function from the chai library to assert the cookie contents. This allows us to easily test cookies in Playwright.

The page object provided by Playwright includes several methods for working with cookies:

- `page.setCookie(cookie)`: Sets a cookie on the page. The cookie argument should be an object with the following properties: `name`, `value`, `url`, `domain`, `path`, `expires`, `httpOnly`, `secure`, `sameSite`, and `priority`.
- `page.deleteCookie(name)`: Deletes a cookie with the given name from the page.
- `page.clearCookies()`: Deletes all cookies from the page.
- `page.cookies()`: Retrieves an array of all cookies from the page.
- 
Here is an example of using these methods to work with cookies in Playwright:

```javascript
const { playwright } = require('playwright')

// Launch a browser instance
const browser = await playwright.chromium.launch()

// Create a new context (i.e. a new incognito window)
const context = await browser.newContext()

// Create a new page
const page = await context.newPage()

// Set a cookie on the page
await page.setCookie({
  name: 'my-cookie',
  value: 'hello world',
})

// Delete a cookie with the given name
await page.deleteCookie('my-cookie')

// Delete all cookies from the page
await page.clearCookies()

// Retrieve an array of all cookies from the page
const cookies = await page.cookies()

// Close the browser instance
await browser.close()
```

In this example, we use the `page.setCookie` method to set a cookie on the page, the `page.deleteCookie` method to delete a cookie, the `page.clearCookies` method to delete all cookies from the page, and the `page.cookies` property to retrieve an array of all cookies from the page. These methods allow us to easily work with cookies in Playwright.

## Testing local storage

Local storage is a web storage feature that allows web applications to store data locally on the user's device, similar to cookies. However, local storage allows web applications to store larger amounts of data, and the data is not automatically included with every HTTP request like cookies are.

Local storage is implemented using the localStorage JavaScript object, which provides methods for setting, retrieving, and removing data from the local storage. For example, the `localStorage.setItem` method can be used to set a value in the local storage, and the `localStorage.getItem` method can be used to retrieve a value from the local storage.

Local storage is typically used to store data that needs to be persisted across sessions, such as user preferences or settings. It can also be used to store data that is too large to be stored in cookies, or data that should not be automatically included with every HTTP request.

To test local storage in Playwright, you can use the `page.evaluate` method to execute JavaScript code that sets and retrieves values from the local storage, and then assert the values using the expect function from the chai library.

Here is an example of how to test local storage in Playwright:

```javascript
const { expect } = require('chai')
const { playwright } = require('playwright')

describe('my tests', () => {
  // Define a test for the local storage
  it('should have the expected values', async () => {
    // Launch a browser instance
    const browser = await playwright.chromium.launch()

    // Create a new context (i.e. a new incognito window)
    const context = await browser.newContext()

    // Create a new page
    const page = await context.newPage()

    // Use the page.evaluate method to execute JavaScript code that sets a value in the local storage
    await page.evaluate(() => {
      // Use the 'localStorage' API to set a value in the local storage
      localStorage.setItem('key', 'value')
    })

    // Use the page.evaluate method to execute JavaScript code that retrieves a value from the local storage
    const value = await page.evaluate(() => {
      // Use the 'localStorage' API to retrieve a value from the local storage
      return localStorage.getItem('key')
    })

    // Use the expect function from the 'chai' library to assert the value from the local storage
    expect(value).to.equal('value')

    // Close the browser instance
    await browser.close()
  })
})
```

In this example, we use the `page.evaluate` method to execute JavaScript code that sets and retrieves values from the local storage using the `localStorage` API.

## Handling Exceptions

In Playwright, you can use the catch method to handle exceptions that are thrown by asynchronous methods like page.click or page.waitFor. This can be useful if you want to handle errors gracefully and continue with your test, rather than allowing the test to fail and stop.

Here is a simple example of how you might use the catch method in Playwright to handle exceptions:

```javascript
const { playwright } = require('playwright');

(async () => {
  const browser = await playwright.chromium.launch();
  const context = await browser.newContext();
  const page = await context.newPage();
  await page.goto('http://localhost:3000');

  try {
    // Wait for the "submit" button to be displayed on the page
    await page.waitFor('button.submit-button');

    // Click the "submit" button
    await page.click('button.submit-button');

    // Wait for the page to navigate to the next page
    await page.waitForNavigation();

    // Assert that the correct page is displayed
    const url = await page.url();
    expect(url).toBe('http://localhost:3000/welcome');
  } catch (error) {
    // Handle the error and continue with the test
    console.error(error);
  }

  await browser.close();
})();
```

In this example, the `try` and `catch` statements are used to handle any exceptions that are thrown by the `waitFor`, `click`, or `waitForNavigation` methods. If an exception is thrown, the error will be logged to the console and the test will continue.

You can use the `catch` method with any asynchronous method in Playwright that may throw an exception, such as `page.fill` or `page.selectOption`. For more information and examples of how to handle exceptions in Playwright, you can refer to the Playwright documentation.

