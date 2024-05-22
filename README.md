BrowserStack Test Observability for WebdriverIO
========


[**BrowserStack Test Observability**](https://www.browserstack.com/test-observability) is a next generation tool which brings together test reporting, precision debugging, flaky test detection and more... all on the same easy to use dashboard.

Test Observability works regardless of if your tests run on BrowserStack, your local machine, or other cloud infrastructure platforms.

![example-test-observability](https://media.giphy.com/media/v1.Y2lkPTc5MGI3NjExMWY0N2NhMjQ2NmRlMzE2ZDljYWYzZmI3Mzc4OGIyMmZmZTgwOWZmMSZjdD1n/Kyd7wYJAANRu6vS2R8/giphy.gif)  


Overview
========
- **Rich Build Insights**: Get better visibility into every single build, and your entire test suite with advanced analytics. Make better decisions with historical data on what tests are failing, flaky or slow.

- **Timeline Debugging**: Time-travel through your test runs with consolidated logs from multiple sources in one single dashboard.

- **Flaky Test Detection**: Automatic detection of flaky tests. Fix flakiness with intelligent suggestions.

- **Seamless Test Re-Runs**: Trigger test re-runs for individual tests or entire builds directly from BrowserStack Test Observability.

- **Smart Failure & Error Analysis**: Spend less time on debugging, as Test Observability intelligently identifies errors and tags tests with their causes of failure.

- **Effortless Integration**: Test Observability integrates with your existing test suite in minutes via the [wdio-browserstack-service](https://webdriver.io/docs/browserstack-service), with zero-code changes necessary.


Getting Started
===============

1. [Sign up](https://www.browserstack.com/users/sign_up?ref=observability) for a free BrowserStack account (no credit card needed!) if you don't already have one.

2. Add the environment variables BROWSERSTACK_USERNAME and BROWSERSTACK_ACCESS_KEY copied from your [account settings](https://www.browserstack.com/accounts/profile).
(Note this will vary by shell, bash and zsh use a common syntax of 
```
export BROWSERSTACK_USERNAME=foo
export BROWSERSTACK_ACCESS_KEY=bar
```)

3. If starting from scratch, initialize a Webdriver.IO project: ` npm init wdio@latest . `

You can use the default selections for most of the configuration wizard:
```html
===============================
🤖 WDIO Configuration Wizard 🧙
===============================

? A project named "wdio-browserstack-test-observability" was detected at (default), correct? Yes
? What type of testing would you like to do? E2E Testing - of Web or Mobile Applications
? Where is your automation backend located? In the cloud using BrowserStack
? Which environment you would like to automate? Web - web applications in the browser
? With which browser should we start? Chrome
? Environment variable for username (username from BrowserStack account in Step 1)
? Environment variable for access key (access key from BrowserStack account)
? Which framework do you want to use? Mocha (https://mochajs.org/)
? Do you want to use a compiler? No!
? Do you want WebdriverIO to autogenerate some test files? Yes
? What should be the location of your spec files? (default location)
? Do you want to use page objects (https://martinfowler.com/bliki/PageObject.html)? Yes
? Where are your page objects located? (default location)
? Which reporter do you want to use? spec
? Do you want to add a plugin to your test setup? (No selection)
? Would you like to include Visual Testing to your setup? For more information see https://webdriver.io/docs/visual-testing! No
? Do you want to add a service to your test setup? browserstack
? Do you want me to run `npm install` Yes
```

4. If using an existing project, copy your username and access key from your [account settings](https://www.browserstack.com/accounts/profile).

5. Install the [`@wdio/browserstack-service`](https://webdriver.io/docs/browserstack-service). Add it as a devDependency in your package.json, via:

```
npm install @wdio/browserstack-service --save-dev

# Use v7.30.1 or later if using WebdriverIO v7 or earlier.
# Use v8.x.x or later if using WebdriverIO v8.
```

6. Configure your `wdio.conf.js` file with code snippets from below depending on where your tests run - on any local or alternative cloud infrastructure, or on BrowserStack. 

7. Run your tests as usual, and visit the [Test Observability dashboard](https://observability.browserstack.com/) to instantly start analyzing and debugging your tests!

You can also [`Read more`](https://www.browserstack.com/docs/test-observability/quick-start/webdriverio#Tests_running_locally_or_elsewhere) in the BrowserStack documentation about how to get started with Test Observability.


Using Test Observability if your tests do not run on BrowserStack
----------------
You can use Test Observability even if you do not want to run your tests on the BrowserStack infrastructure. Your tests could be running on a CI or on your laptop or even on other cloud service providers like Sauce Labs, however, Test Observability will still work and give you all the intelligent test reports, debugging capabilities and advanced analytics you need!

You can set your config in the following manner if you do not want to run tests on BrowserStack Automate or App Automate (BrowserStack infrastructure), but still want to use Test Observability (note that `user` and `key` are now defined under the scope of the `browserstack` service). Ensure that the `testObservability` flag is set to `true`, and specify a static `projectName` and `buildName` under `testObservabilityOptions`. Test Observability will automatically recognize new builds of the same project/build name and start populating the dashboard with your builds when you run your tests.

```js
// wdio.conf.js
export const config = {
    // ...
    services: [
        ['browserstack', {
            testObservability: true,
            testObservabilityOptions: {
                user: process.env.BROWSERSTACK_USERNAME,
                key: process.env.BROWSERSTACK_ACCESS_KEY,
                projectName: "Your project name goes here",
                buildName: "The static build job name goes here e.g. Nightly regression"
            }
        }]
    ],
    // ...
};
```


Using Test Observability if your tests are already running on BrowserStack
----------------

If you are already running tests on BrowserStack, you likely already have the @wdio/browserstack-service set up. Ensure that the `testObservability` flag is set to `true`, and specify a static `projectName` and `buildName` under `testObservabilityOptions`. Test Observability will automatically recognize new builds of the same project/build name and start populating the dashboard with your builds when you run your tests.

```js
// wdio.conf.js
export const config = {
    // ...
    user: process.env.BROWSERSTACK_USERNAME,
    key: process.env.BROWSERSTACK_ACCESS_KEY,
    services: [
        ['browserstack', {
            testObservability: true,
            testObservabilityOptions: {
                projectName: "Your project name goes here",
                buildName: "The static build job name goes here e.g. Nightly regression"
            },
            browserstackLocal: true
        }]
    ],
    // ...
};
```

