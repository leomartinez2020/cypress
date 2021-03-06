# Cypress
All things Cypress - End to end testing

## What is Cypress?

Cypress is an end-to-end testing framework. It includes an assertion library, mocking and stubbing. All without Selenium, they claim.

Cypress uses javascript as the main and only language.

## Differences with Selenium

Both are automation frameworks. Selenium uses the Webdriver protocol which is an HTTP Rest Json protocol for sending commands. The debugger can control the browser, like Chrome DevTools. All interactions with the browser, like mouse clicks, happen through HTTP requests. Selenium runs on all browsers. The communication with the browser is one directional.

On the other hand, Cypress is able to respond to events on the browser because it is executed in the same run loop as the applications running on the browser (Cypress runs inside the browser). Cypress is able to capture network traffic. It is easy to take screenshots and record videos of the interactions with the browser.

Cypress avoids flakiness by waiting for elements to be visible or for events to be triggered.

## Installation

```
npm init -y
npm install cypress --save-dev
```
To open the test runner use the command

```
npx cypress open
```
Or this command for CI:
```
./node_modules/.bin/cypress open
```
Or this one:
```
$(npm bin)/cypress open

```

When the test runner launches it creates a folder called *cypress*. The tests are found inside a folder called *integration*

## Writing a test:

```
/// <reference types="Cypress" />

describe('My First Test', () => {
  it('Does not do much!', () => {
    expect(true).to.equal(true)
  })
})

```
 
 ## Command chaining

Some commands yield a DOM element and thus can be chained to ther commands:
```
cy.get('#button).should('contain', 'submit').and('have.class', 'btn').click();
```

If the command yields *null*, it cannot be chainable:
```
cy.clearCookies();
```

## Closures

Due to the asynchronous nature of cypress, this is not possible:

```
const button = cy.get('#button');
button.click();
```

You have to chain the commands:
```
cy.get('#button').click();
```

Another option is to use *then()*

```
cy.get('#button').then(($btn) => {
  expect($btn.text())to.be.a.('string');
});
```