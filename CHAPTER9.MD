# Chapter 9 - Common Testing Scenarios

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

## Testing Peformance

o test performance in Playwright, you can use the `page.metrics` property to access performance metrics, such as the time to first paint or the time to first contentful paint. You can then assert the values of these metrics using the expect function from the chai library.

Here is an example of how to test performance in Playwright:

```javascript
const { expect } = require('chai')
const { playwright } = require('playwright')

describe('my tests', () => {
  // Define a test for the performance metrics
  it('should have the expected values', async () => {
    // Launch a browser instance
    const browser = await playwright.chromium.launch()

    // Create a new context (i.e. a new incognito window)
    const context = await browser.newContext()

    // Create a new page
    const page = await context.newPage()

    // Navigate to a website
    await page.goto('https://www.example.com')

    // Use the page.metrics property to access the performance metrics
    const metrics = await page.metrics()

    // Use the expect function from the 'chai' library to assert the performance metrics
    expect(metrics.timestamp).to.be.a('number')
    expect(metrics.timings).to.be.an('object')
    expect(metrics.timings.firstPaint).to.be.a('number')
    expect(metrics.timings.firstContentfulPaint).to.be.a('number')

    // Close the browser instance
    await browser.close()
  })
})
```

In this example, we use the `page.metrics` property to access the performance metrics for the page, and then use the expect function from the chai library to assert the values of the metrics. This allows us to easily test the performance of a page in Playwright.

## Testing Accessibility

Yes, Playwright supports accessibility testing through the `Accessibility` class, which provides methods for retrieving accessibility information from a page and asserting it using the `expect` function from the chai library.

Here is an example of how to test accessibility in Playwright:

```javascript
const { expect } = require('chai')
const { playwright } = require('playwright')

describe('my tests', () => {
  // Define a test for accessibility
  it('should be accessible', async () => {
    // Launch a browser instance
    const browser = await playwright.chromium.launch()

    // Create a new context (i.e. a new incognito window)
    const context = await browser.newContext()

    // Create a new page
    const page = await context.newPage()

    // Navigate to a website
    await page.goto('https://www.example.com')

    // Create an instance of the Accessibility class
    const accessibility = new Accessibility(context)

    // Use the accessibility.snapshot method to retrieve the accessibility information for the page
    const snapshot = await accessibility.snapshot({
      interestingOnly: false,
    })

    // Use the expect function from the 'chai' library to assert the accessibility information
    expect(snapshot).to.satisfyA11yStandards()

    // Close the browser instance
    await browser.close()
  })
})
```

In this example, we use the `Accessibility` class to create an instance of the `accessibility` object, and then use the `accessibility.snapshot` method to retrieve the accessibility information for the page. We then use the expect function from the chai library to assert that the accessibility information satisfies the accessibility standards. This allows us to easily test the accessibility of a page in Playwright.

## Testing Visual Regression

Visual regression testing is a technique used to detect changes in the visual appearance of a website or application. It involves taking screenshots of a website or application, and then comparing the screenshots to previous versions to detect any visual changes or differences.

Visual regression testing can be used to ensure that changes to a website or application do not introduce visual regressions, such as changes to the layout, styling, or positioning of elements. It can also be used to verify that the appearance of a website or application remains consistent across different browsers, devices, or screen sizes.

Visual regression testing is typically performed using specialized tools that automate the process of taking screenshots and comparing them to previous versions. These tools can help to identify visual regressions quickly and accurately, allowing developers to fix any issues before they are released to users.

Playwright supports visual regression testing through the `playwright-to-png` library, which allows you to take screenshots of a page in Playwright and compare them to previous screenshots to detect visual changes. However, there are various other visual regression vendors who support Playwright.

Here is an example of how to perform visual regression testing in Playwright:

```javascript
const { playwright } = require('playwright')
const toPng = require('playwright-to-png')

describe('my tests', () => {
  // Define a test for visual regression
  it('should not have visual regressions', async () => {
    // Launch a browser instance
    const browser = await playwright.chromium.launch()

    // Create a new context (i.e. a new incognito window)
    const context = await browser.newContext()

    // Create a new page
    const page = await context.newPage()

    // Navigate to a website
    await page.goto('https://www.example.com')

    // Take a screenshot of the page
    const screenshot = await toPng(page)

    // Compare the screenshot to the expected screenshot
    expect(screenshot).to.matchImageSnapshot()

    // Close the browser instance
    await browser.close()
  })
})
```

In this example, we use the `playwright-to-png` library to take a screenshot of the page using the `toPng` function, and then use the expect function from the chai library to compare the screenshot to the expected screenshot. This allows us to easily perform visual regression testing in Playwright.

## Testing on Mobile devices

Yes, Playwright supports testing on mobile devices through the `deviceDescriptors` module, which provides device descriptors for a variety of popular mobile devices.

To test on a mobile device in Playwright, you can use the `playwright.devices` object to retrieve the device descriptor for the device you want to test on, and then pass the device descriptor to the launch or connect method of the playwright object when creating the browser or browser context.

Here is an example of how to test on a mobile device in Playwright:

```javascript
const { playwright } = require('playwright')

// Use the playwright.devices object to retrieve the device descriptor for the iPhone 6
const iPhone6 = playwright.devices['iPhone 6']

// Launch a browser instance that simulates the iPhone 6
const browser = await playwright.chromium.launch({
  headless: false,
  device: iPhone6,
})

// Create a new context (i.e. a new incognito window) that simulates the iPhone 6
const context = await browser.newContext({
  device: iPhone6,
})

// Create a new page that simulates the iPhone 6
const page = await context.newPage({
  device: iPhone6,
})

// Navigate to a website
await page.goto('https://www.example.com')

// Close the browser instance
await browser.close()
```

In this example, we use the `playwright.devices` object to retrieve the device descriptor for the iPhone 6, and then pass the device descriptor to the launch and `newContext` methods when creating the browser and context. This allows Playwright to simulate the iPhone 6 when running the tests, allowing us to easily test on mobile devices.
