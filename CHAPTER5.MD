# Chapter 5 - Performing Keyboard and Mouse Events

> **Note** 
> Plagiarism detected by Grammarly - 6%

## Performing keyboard events

The `page.keyboard` object in Playwright is used to simulate keyboard events on a web page, such as typing text or pressing keys. It provides a number of methods and properties that you can use to interact with the keyboard in your tests or other code.

For example, the `page.keyboard.press` method can be used to press a specific key on the keyboard, such as the Enter or Tab key. The `page.keyboard.type` method can be used to simulate typing text, including special characters and modifier keys like Ctrl or Alt. The `page.keyboard.down` and `page.keyboard.up` methods can be used to simulate pressing and releasing a specific key.

In addition, the `page.keyboard` object provides properties that you can use to configure the behavior of keyboard events, such as the `page.keyboard.delay` property, which specifies the delay between key presses when typing text, or the `page.keyboard.autoRepeatDelay` property, which specifies the delay before auto-repeating a held key.

Overall, the `page.keyboard` object in Playwright provides a powerful set of tools for simulating keyboard events on a web page, and can be used to automate a wide range of interactions and tests.

To press keys, such as the Enter or Tab key, on a web page using Playwright, you can use the `page.keyboard.press` method, as shown in the following example:

```javascript
const playwright = require('playwright');

(async () => {
  // Start a new browser instance
  const browser = await playwright.chromium.launch();

  // Create a new page
  const page = await browser.newPage();

  // Navigate to a web page
  await page.goto('https://example.com');

  // Find the input field on the page
  const input = await page.$('#some-input');

  // Type "Hello, world!" into the input field
  await input.type('Hello, world!');

  // Press the Tab key to move focus to the next element
  await page.keyboard.press('Tab');

  // Press the Enter key to submit the form
  await page.keyboard.press('Enter');

  // Close the browser
  await browser.close();
})();
```

In this example, the `playwright.chromium.launch` method is used to start a new browser instance, and the `browser.newPage` method is used to create a new page. The `page.goto` method is then used to navigate to a web page, and the `page.$` method is used to find the input field on the page.

Once the input field is found, the input.type method is used to type "Hello, world!" into the field. Then, the `page.keyboard.press` method is used to press the Tab key to move focus to the next element on the page. Finally, the `page.keyboard.press` method is used again, this time to press the Enter key to submit the form.

Finally, the `browser.close` method is used to close the browser instance and clean up any resources.

To simulate copy and paste keyboard events, such as Ctrl + C and Ctrl + V, on a web page using Playwright, you can use the `page.keyboard.type` method, as shown in the following example:

```javascript
const playwright = require('playwright');

(async () => {
  // Start a new browser instance
  const browser = await playwright.chromium.launch();

  // Create a new page
  const page = await browser.newPage();

  // Navigate to a web page
  await page.goto('https://example.com');

  // Find the input field on the page
  const input = await page.$('#some-input');

  // Type "Hello, world!" into the input field
  await input.type('Hello, world!');

  // Select the text in the input field
  await input.selectText();

  // Simulate pressing Ctrl + C to copy the text
  await page.keyboard.type('^C');

  // Find the textarea on the page
  const textarea = await page.$('#some-textarea');

  // Focus the textarea
  await textarea.focus();

  // Simulate pressing Ctrl + V to paste the copied text
  await page.keyboard.type('^V');

  // Close the browser
  await browser.close();
})();
```
In this example, the `playwright.chromium.launch` method is used to start a new browser instance, and the `browser.newPage` method is used to create a new page. The `page.goto` method is then used to navigate to a web page, and the `page.$` method is used to find the input field and textarea on the page.

Once the input field and textarea are found, the `input.type` method is used to type "Hello, world!" into the input field. Then, the `input.selectText` method is used to select the text in the input field, and the `page.keyboard.type` method is used to simulate pressing Ctrl + C to copy the text.

Next, the `textarea.focus` method is used to focus the textarea, and the `page.keyboard.type` method is used again, this time to simulate pressing Ctrl + V to paste the copied

## Performing Mouse Events

In Playwright, you can use the page.mouse object to simulate mouse events, such as clicking, double-clicking, or hovering over an element on a web page. This can be useful if you want to test the behavior of a web application in response to these events.

Here is a simple example of how you might use the `page.mouse` object in Playwright to perform mouse events:

```javascript
const { playwright } = require('playwright');

(async () => {
  const browser = await playwright.chromium.launch();
  const context = await browser.newContext();
  const page = await context.newPage();
  await page.goto('http://localhost:3000');

  // Click an element on the page
  await page.mouse.click(100, 100);

  // Double-click an element on the page
  await page.mouse.doubleClick(200, 200);

  // Hover over an element on the page
  await page.mouse.move(300, 300);

  await browser.close();
})();
```

In this example, the `page.mouse` object is used to simulate a click, double-click, and hover over an element on the page. The `click` and `doubleClick` methods take the x and y coordinates of the element as arguments, and the `move` method takes the coordinates of the element to hover over.

The `page.mouse` object in Playwright provides several methods for simulating mouse events on a web page. These methods include:

- `page.mouse.click(x, y, options)`: This method simulates a click at the specified coordinates on the page. The options argument can be used to specify modifier keys like Shift or Alt.
- `page.mouse.doubleClick(x, y, options)`: This method simulates a double-click at the specified coordinates on the page. The options argument can be used to specify modifier keys like Shift or Alt.
- `page.mouse.down(x, y, options)`: This method simulates pressing the left mouse button at the specified coordinates on the page. The options argument can be used to specify modifier keys like Shift or Alt.
- `page.mouse.move(x, y, options)`: This method simulates moving the mouse cursor to the specified coordinates on the page. The options argument can be used to specify modifier keys like Shift or Alt.
- `page.mouse.up(x, y, options)`: This method simulates releasing the left mouse button at the specified coordinates on the page. The options argument can be used to specify modifier keys like Shift or Alt.

These are just a few examples of the methods that the `page.mouse` object provides in Playwright.

## Performing Drag and Drop

In Playwright, you can use the `page.drag` and `page.drop` methods to simulate a drag and drop operation on a web page. This can be useful if you want to test the behavior of a web application when an element is dragged and dropped onto another element.

Here is a simple example of how you might use the `page.drag` and `page.drop` methods in Playwright to perform a drag and drop operation:

```javascript
const { playwright } = require('playwright');

(async () => {
  const browser = await playwright.chromium.launch();
  const context = await browser.newContext();
  const page = await context.newPage();
  await page.goto('http://localhost:3000');

  // Get the coordinates of the source element
  const source = await page.$('#source');
  const { x: sourceX, y: sourceY } = await source.boundingBox();

  // Get the coordinates of the target element
  const target = await page.$('#target');
  const { x: targetX, y: targetY } = await target.boundingBox();

  // Drag the source element to the target element
  await page.drag(sourceX, sourceY, targetX, targetY);
  await page.drop();

  await browser.close();
})();
```

In this example, the `page.drag` method is used to simulate dragging the source element to the target element on the page. The `page.drag` method takes the x and y coordinates of the source element and the target element as arguments, and simulates moving the mouse cursor from the source coordinates to the target coordinates.

Once the drag operation has been simulated, the `page.drop` method is called to simulate releasing the mouse button, completing the drag and drop operation.

## Performing chain of Keyboard and Mouse events

In Playwright, you can use the `page.keyboard` and `page.mouse` objects to simulate complex mouse and keyboard events on a web page. This can be useful if you want to test the behavior of a web application in response to these events, such as dragging and dropping an element while holding down a modifier key like Shift or Alt.

Here is a simple example of how you might use the `page.keyboard` and `page.mouse` objects in Playwright to perform complex mouse and keyboard events:

```javascript
const { playwright } = require('playwright');

(async () => {
  const browser = await playwright.chromium.launch();
  const context = await browser.newContext();
  const page = await context.newPage();
  await page.goto('http://localhost:3000');

  // Press the Shift key
  await page.keyboard.down('Shift');

  // Get the coordinates of the source element
  const source = await page.$('#source');
  const { x: sourceX, y: sourceY } = await source.boundingBox();

  // Get the coordinates of the target element
  const target = await page.$('#target');
  const { x: targetX, y: targetY } = await target.boundingBox();

  // Drag the source element to the target element
  await page.mouse.move(sourceX, sourceY);
  await page.mouse.down();
  await page.mouse.move(targetX, targetY);
  await page.mouse.up();

  // Release the Shift key
  await page.keyboard.up('Shift');

  await browser.close();
})();
```

In this example, the `page.keyboard.down` and `page.keyboard.up` methods are used to press and release the Shift key, respectively. This simulates holding down the Shift key while performing a drag and drop operation using the `page.mouse` object.

The page.mouse object is used to simulate moving the mouse cursor to the source element, pressing the left mouse button, moving the mouse cursor to the target element, and releasing the mouse button. This simulates dragging the source element to the target element on the page.
