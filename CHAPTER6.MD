# Chapter 6 - Interacting with Page

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
