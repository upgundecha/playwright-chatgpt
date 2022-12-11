# Chapter 10 - Design Patterns

## Playwright Design Patterns

Playwright supports several common design patterns that can be used when writing tests. These patterns include the page object pattern, the page fragment pattern, the data-driven testing pattern, and the behavior-driven development (BDD) pattern.

The page object pattern is a design pattern that separates the page-specific logic and elements from the tests, and provides a high-level API for interacting with the page. This allows the tests to be written in a more readable and maintainable way, and makes it easier to update the tests when the page changes.

The page fragment pattern is a design pattern that breaks down a page into smaller, reusable fragments, such as a header or footer. This allows the tests to focus on specific parts of the page, and makes it easier to reuse the fragments in multiple tests.

The data-driven testing pattern is a design pattern that allows the tests to be parameterized, so that the same test can be run multiple times with different input data. This allows the tests to be more comprehensive and cover a wider range of scenarios.

The behavior-driven development (BDD) pattern is a design pattern that focuses on the behavior of the system being tested, rather than the implementation details. This allows the tests to be written in a more natural and human-readable language, and makes it easier for stakeholders to understand and collaborate on the tests.

## The Page Object Design Pattern

The page object pattern is a design pattern that separates the page-specific logic and elements from the tests, and provides a high-level API for interacting with the page. This allows the tests to be written in a more readable and maintainable way, and makes it easier to update the tests when the page changes.

Here is an example of how to use the page object pattern in Playwright:

```javascript
// Define a page object class for the login page
class LoginPage {
  constructor(page) {
    this.page = page
  }

  // Define a method that fills in the username and password fields and clicks the login button
  async login(username, password) {
    // Fill in the username field
    await this.page.fill('#username', username)

    // Fill in the password field
    await this.page.fill('#password', password)

    // Click the login button
    await this.page.click('#login')
  }
}

// Define a test that uses the page object
describe('my tests', () => {
  it('should be able to login', async () => {
    // Launch a browser instance
    const browser = await playwright.chromium.launch()

    // Create a new context (i.e. a new incognito window)
    const context = await browser.newContext()

    // Create a new page
    const page = await context.newPage()

    // Navigate to the login page
    await page.goto('https://www.example.com/login')

    // Create an instance of the LoginPage class
    const loginPage = new LoginPage(page)

    // Use the login method of the LoginPage class to log in
    await loginPage.login('username', 'password')

    // Close the browser instance
    await browser.close()
  })
})
```

In this example, we define a `LoginPage` class that provides a `login` method for logging in to the page. We then use the `LoginPage` class in the test, creating an instance of the `LoginPage` class and calling the `login` method to log in. This allows us to separate the page-specific logic and elements from the tests, making the tests more readable and maintainable.

## Implementing BDD using Cucumber

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
```

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
5. Create a new file in your project directory and name it index.js. This will be the main script file for your Cucumber tests.

6. Open the file in your code editor and add the following code to it:

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

You can use Cucumber with Playwright to define and automate acceptance tests for your web application. This can help ensure that your application behaves as expected and meets the needs of your users.

