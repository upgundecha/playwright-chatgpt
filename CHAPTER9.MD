# Chapter 9 - Advanced Topics

## Mocking API's during testing

Playwright does not include any built-in support for mocking APIs during testing. However, it is possible to use external libraries and tools to mock APIs and test how a web page interacts with them.

Here is an example of how to use the nock library to mock an API and test a web page using Playwright:

```javascript
const { expect } = require('chai')
const nock = require('nock')
const { playwright } = require('playwright')

describe('my tests', () => {
  // Define a test for the web page
  it('should do something with the API response', async () => {
    // Mock the API using nock
    nock('https://www.example.com/api')
      .get('/endpoint')
      .reply(200, { data: 'mock data' })

    // Launch a browser instance
    const browser = await playwright.chromium.launch()

    // Create a new context (i.e. a new incognito window)
    const context = await browser.newContext()

    // Create a new page
    const page = await context.newPage()

    // Navigate to the web page
    await page.goto('https://www.example.com/')

    // Use the page.evaluate method to execute JavaScript code that interacts with the API
    const response = await page.evaluate(() => {
      // Send a request to the API and return the response
      return fetch('https://www.example.com/api/endpoint')
        .then(res => res.json())
    })

    // Use the expect function from the 'chai' library to assert the response from the API
    expect(response).to.deep.equal({ data: 'mock data' })

    // Close the browser instance
    await browser.close()
  })
})
```

In this example, we use the nock library to mock an API and return a predetermined response. We then use Playwright to launch a browser instance, navigate to a web page, and

## Testing REST APIs

Playwright does not include any built-in support for testing REST APIs. However, it is possible to use external libraries and tools, such as the node-fetch library, to send requests to a REST API and test the responses.

Here is an example of how to use the node-fetch library to test a REST API using Playwright:

```javascript
const { expect } = require('chai')
const fetch = require('node-fetch')
const { playwright } = require('playwright')

describe('my tests', () => {
  // Define a test for the REST API
  it('should return the correct response', async () => {
    // Send a request to the REST API using the fetch function from the 'node-fetch' library
    const response = await fetch('https://www.example.com/api/endpoint')
    const data = await response.json()

    // Use the expect function from the 'chai' library to assert the response from the API
    expect(data).to.deep.equal({ data: 'expected data' })
  })
})
```

In this example, we use the `node-fetch` library to send a request to the REST API and verify the response. We use the expect function from the chai library to assert that the response has the expected status code, headers, and body.

Note that this approach only allows us to test the responses from the API, and does not provide a way to test the functionality of the API itself. To test the functionality of a REST API, it is recommended to use a dedicated testing framework or library that is designed specifically for that purpose.

