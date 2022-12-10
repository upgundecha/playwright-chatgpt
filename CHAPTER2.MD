# Chapter 2 - Getting Started

## How to setup Playwright development environment?

To set up a Playwright development environment, you will need to install a few things first. Here is a step-by-step guide:

1. Install Node.js and npm (the Node.js package manager) on your computer. You can download and install them from the official Node.js website (https://nodejs.org/en/).
2. Create a new directory for your project and navigate to it in the terminal or command prompt.
3. Install Playwright and its dependencies by running the following command:

```
npm install playwright
```

4. Install a code editor or IDE of your choice. Some popular options include Visual Studio Code, Atom, and Sublime Text.
5. Create a new file in your project directory and name it index.js. This will be the main script file for your Playwright tests.
6. Open the file in your code editor and add the following code to it:

```javascript
const playwright = require('playwright');

(async () => {
  // Your Playwright code goes here
})();
```

7. Save the file and run it using the following command:

```
node index.js
```

This should set up a basic Playwright development environment on your computer. You can now start writing your tests using the Playwright API.

## How to navigate to Google and search using Playwright?

To navigate to Google and perform a search using Playwright, you will need to use the Playwright API to control a web browser. Here is an example of how you could do this:

```javascript
const playwright = require('playwright');

(async () => {
  // Start a new browser instance
  const browser = await playwright.chromium.launch();

  // Create a new page
  const page = await browser.newPage();

  // Navigate to Google
  await page.goto('https://www.google.com/');

  // Type a search query into the search box
  await page.fill('input[name="q"]', 'Playwright');

  // Submit the search form
  await page.click('input[type="submit"]');

  // Wait for the search results to load
  await page.waitForSelector('#search');

  // Close the browser
  await browser.close();
})();
```

This code will start a new browser instance, navigate to Google, enter a search query, submit the search form, and wait for the results to load. It will then close the browser.
Note that this is just a simple example to illustrate how to navigate to Google and perform a search using Playwright. You may need to adjust the code to fit your specific needs.

## Which testing frameworks are supported by Playwright?

Playwright is a low-level library for automating web browsers, so it does not come with a built-in testing framework. However, it can be used with any testing framework that supports JavaScript, such as Mocha, Jest, or Jasmine.

Here is an example of how you could use Playwright with the Mocha testing framework:

```javascript
const playwright = require('playwright');
const assert = require('assert');

describe('My Playwright tests', () => {
  it('should do something', async () => {
    // Start a new browser instance
    const browser = await playwright.chromium.launch();

    // Create a new page
    const page = await browser.newPage();

    // Do something with the page

    // Assert something about the page
    assert(true);

    // Close the browser
    await browser.close();
  });
});
```
In this example, the `describe` and `it` functions are provided by Mocha, and the `assert` function is provided by the `assert module`. Playwright is used to control the browser and interact with the page.
You can use Playwright with any testing framework that supports JavaScript in a similar way. Just be sure to install the testing framework and any necessary dependencies before running your tests.

## Playwright and Jest

Here is an example of a Google search test case using Playwright and Jest:

```javascript
const playwright = require('playwright');

describe('Google search', () => {
  it('should show results for Playwright', async () => {
    // Start a new browser instance
    const browser = await playwright.chromium.launch();

    // Create a new page
    const page = await browser.newPage();

    // Navigate to Google
    await page.goto('https://www.google.com/');

    // Type a search query into the search box
    await page.fill('input[name="q"]', 'Playwright');

    // Submit the search form
    await page.click('input[type="submit"]');

    // Wait for the search results to load
    await page.waitForSelector('#search');

    // Check if the page contains the expected text
    const text = await page.evaluate(() => document.body.textContent);
    expect(text).toContain('Playwright');

    // Close the browser
    await browser.close();
  });
});
```

This test case uses Playwright to control the browser and interact with the page, and Jest to structure the test and make assertions about the page. It navigates to Google, performs a search for "Playwright", and checks if the page contains the expected text.
Note that this is just a simple example to illustrate how to use Playwright and Jest together. You may need to adjust the code to fit your specific needs. For example, you may want to add more test cases or make more detailed assertions about the page.

## Playwright and Cucumber

Cucumber is a tool for behavior-driven development (BDD) that allows developers to define and automate acceptance tests. It uses a language called Gherkin to define test cases in a natural, human-readable language.

Here is an example of a simple Cucumber test using Gherkin:

```gherkin
Feature: Google search
  As a user
  I want to search for things on Google
  So that I can find what I'm looking for

  Scenario: Search for Playwright
    Given I am on the Google homepage
    When I search for "Playwright"
    Then the page should contain "Playwright"
``
This test defines a feature called "Google search", which describes the functionality that the test is testing. It then defines a scenario called "Search for Playwright", which describes the steps that the test will take. The steps are written in Gherkin and use a natural language to describe what the test will do.

To use Cucumber with Playwright, you will need to install both libraries in your project. Here is a step-by-step guide:

1. Install Node.js and npm (the Node.js package manager) on your computer. You can download and install them from the official Node.js website (https://nodejs.org/en/).
2. Create a new directory for your project and navigate to it in the terminal or command prompt.
3. Install Playwright and its dependencies by running the following command:
```
npm install playwright
```
4. Install Cucumber and its dependencies by running the following command:
```
npm install cucumber
```
Create a new file in your project directory and name it index.js. This will be the main script file for your Cucumber tests.

Open the file in your code editor and add the following code to it:
```javascript
const { Given, When, Then } = require('cucumber');
const playwright = require('playwright');

Given('I am on the Google homepage', async function() {
  // Start a new browser instance
  this.browser = await playwright.chromium.launch();

  // Create a new page
  this.page = await this.browser.newPage();

  // Navigate to Google
  await this.page.goto('https://www.google.com/');
});

When('I search for {string}', async function(query) {
  // Type the search query into the search box
  await this.page.fill('input[name="q"]', query);

  // Submit the search form
  await this.page.click('input[type="submit"]');

  // Wait for the search results to load
  await this.page.waitForSelector('#search');
});

Then('the page should contain {string}', async function(text) {
  // Check if the page contains the expected text
  const pageText = await this.page.evaluate(() => document.body.textContent);
  expect(pageText).toContain(text);

  // Close the browser
  await this.browser.close();
});
```
This code defines a simple Cucumber test that uses Playwright to control the browser and interact with the page. It navigates to Google, performs a search, and checks if the page contains the expected text.

7. Save the file and run it using the following command:
```
node index.js
```
This code defines a Cucumber test that uses Playwright to control the browser and interact with the page. It navigates to Google, performs a search, and checks if the page contains the expected text.

You can use Cucumber with Playwright to define and automate acceptance tests for your web application. This can help ensure that your application behaves as expected and meets the needs of your users.
