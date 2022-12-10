# Chapter 3 - Finding Elements

## How does Playwright identifies HTML elements?

Playwright uses CSS selectors to identify HTML elements on a web page. CSS selectors are patterns that match specific elements based on their attributes and relationship to other elements in the page.

For example, if you want to click on a button with the text "Submit" on a web page using Playwright, you could use the following CSS selector:

```
button[type="submit"]
```

This selector will match any `button` element on the page with a `type` attribute set to "submit". Playwright will then use this selector to locate the element on the page and perform the desired action, such as clicking on it.

You can use a wide variety of CSS selectors to identify different types of elements on the page. For example, you can use class and ID selectors to match elements based on their class and ID attributes, respectively. You can also use attribute selectors to match elements based on their attribute values, and combinators to match elements based on their relationship to other elements in the page.

Playwright also provides a number of convenience methods that allow you to easily find elements on the page without needing to know the exact CSS selector for the element. For example, you can use the page.$ method to find an element by its text content, or the page.$$ method to find multiple elements that match a given selector.

1. `page.$(selector)`: This method finds the first element on the page that matches the given CSS selector. For example, `page.$('button[type="submit"]')` will find the first button element on the page with a `type` attribute set to "submit".
2. `page.$$(selector)`: This method finds all elements on the page that match the given CSS selector. For example, `page.$$('a')` will find all `a `(link) elements on the page.
3. `page.$eval(selector, pageFunction)`: This method evaluates the given page function for the first element on the page that matches the given CSS selector. The page function can be any JavaScript code that you want to run in the context of the page. For example, `page.$eval('button[type="submit"]', button => button.click())` will find the first button element on the page with a `type` attribute set to "submit" and click on it.
4. `page.$$eval(selector, pageFunction)`: This method evaluates the given page function for all elements on the page that match the given CSS selector. The page function can be any JavaScript code that you want to run in the context of the page. For example,`page.$$eval('a', links => links.forEach(link => link.click()))` will find all ` a` (link) elements on the page and click on each of them.

Overall, these different locator strategies allow you to easily find and interact with elements on the page using CSS selectors and JavaScript code. They are a powerful and flexible way to automate your tests with Playwright.

## Examples of CSS selectors in Playwright

Here are some examples of CSS selectors that you can use to identify elements on a web page with Playwright:

- `button`: This selector will match any `button` element on the page.
- `button[type="submit"]`: This selector will match any `button` element on the page with a `type` attribute set to "submit".
- `#submit-button`: This selector will match any element on the page with an `ID` attribute set to "submit-button".
- `.submit-button`: This selector will match any element on the page with a `class` attribute set to "submit-button".
- `form input`: This selector will match any `input` element that is a descendant of a `form` element on the page.
- `form > input`: This selector will match any `input` element that is a direct child of a `form` element on the page.

These are just a few examples of the many different CSS selectors that you can use with Playwright. You can use a wide variety of CSS selectors to match elements based on their attributes, relationships to other elements, and other criteria. You can also use combinators and pseudo-classes to create more complex and powerful selectors.

Overall, CSS selectors are a powerful and flexible way to identify HTML elements on a web page, and Playwright makes it easy to use them in your tests.
