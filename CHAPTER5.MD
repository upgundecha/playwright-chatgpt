# Chapter 5 - Mouse and Keyboard Actions

## How to perform keyboard events

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


