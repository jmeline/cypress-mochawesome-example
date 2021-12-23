# Getting Started with Create React App + Cypress + Mochawesome

## Install 
* Create-react-app
```
$ npx create-react-app cypress-mocawesome-example --template cra-template-typescript
```
* Cypress
```
$ npm i -D cypress
```
* Mochawesome
```
$ npm i -D mocha mochawesome mochawesome-merge mochawesome-report-generator
```
* extra package(s)
```
$ npm i -D rimraf
```

* Open Cypress && Write your tests
```
$ npm run cy:open
```
Opening cypress and running the examples builds all the directories in cypress. Helpful but not needed

```
$ mkdir cypress/integration/App
$ touch cypress/integration/App/App.spec.js
```
## Configuration
* Edit package.json and add scripts to support mochawesome
```json
{
  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test",
    "eject": "react-scripts eject",
    "cy:run": "cypress run -C cypress/cypress.json",
    "cy:open": "cypress open -C cypress/cypress.json",
    "cy:test": "npm run cy:run && npm run posttest",
    "clean:reports": "rimraf cypress/reports && mkdir cypress\\reports && mkdir cypress\\reports\\mochareports",
    "combine-reports": "mochawesome-merge cypress/reports/mocha/*.json > cypress/reports/mochareports/report.json",
    "generate-report": "marge cypress/reports/mochareports/report.json -f report -o cypress/reports/mochareports",
    "posttest": "npm run combine-reports && npm run generate-report",
    "pretest": "npm run clean:reports"
  }
}
```
* Add mochawesome settings to cypress/cypress.json (feel free to move the cypress.json in the project directory, remember to update package.json scripts if you do)
```json
{
  "testFiles": "**/*.spec.{js,ts,jsx,tsx}",
  "reporter": "mochawesome",
  "reporterOptions": {
    "reportDir": "cypress/reports/mocha",
    "quite": true,
    "overwrite": false,
    "html": false,
    "json": true
  }
} 
```
## Add tests (if you want)
* Add a test in the integration directory (see [writing first test](https://on.cypress.io/writing-first-test) for more info)
    - You can skip this and use the example integrations.
```
// cypress/integration/App/App.spec.js
describe("App", () => {
    it("checks that the link text is shown", () => {
        expect(true).to.equal(true)
    })
})
```
## Run tests and create reports

```
$ npm run cy:test
```

I left in the examples so that I could have multiple reports generated.

![image](https://user-images.githubusercontent.com/6642964/147273469-c141aead-dfdc-49ed-a956-ecf0b6729bb9.png)

## View Report
All these reports are then merged into a single beautiful html report located here: cypress\reports\mochareports\report.html

![image](https://user-images.githubusercontent.com/6642964/147271860-4043c981-eb94-4373-bddb-3486c70c5e1b.png)

Done :)

I found that mochawesome works with older versions of Cypress. We had v5.6.0 at work and mochawesome worked fine with this version as well as the newer 9.2.0.

You can learn more in the [Create React App documentation](https://facebook.github.io/create-react-app/docs/getting-started).

To learn React, check out the [React documentation](https://reactjs.org/).
