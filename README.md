# ng-apimock/cypress-plugin [![CircleCI](https://circleci.com/gh/ng-apimock/cypress-plugin.svg?style=svg)](https://circleci.com/gh/ng-apimock/cypress-plugin)  [![dependency Status](https://img.shields.io/david/ng-apimock/cypress-plugin.svg)](https://david-dm.org/ng-apimock/cypress-plugin) [![devDependency Status](https://img.shields.io/david/dev/ng-apimock/cypress-plugin.svg)](https://david-dm.org/ng-apimock/cypress-plugin#info=devDependencies)
The cypress plugin for ng-apimock. 

### Usage
This plugin connects to ng-apimock and makes the plugin functions available within the tests.

1. Enable this plugin in your supports file:

```js
require('@ng-apimock/cypress-plugin').load();
```

2. Add environment variables to `cypress.json` configuration file

Use **NG_API_MOCK_ENABLE_LOGS** with a string value of "true" or "false". Default: "true".
Use **NG_API_MOCK_BASE_URL** with a string value of base url of your ng-apimock server

```json
{
  "env": {
    "NG_API_MOCK_BASE_URL": "http://localhost:3000",
    "NG_API_MOCK_ENABLE_LOGS": "false"
  }
}
```

3. After registering the plugin and adding environment variables to Cypress config, you can use it in your tests by calling it like this:

```js
describe('Some test', () => {
    it('does something', () => 
        cy.selectScenario('my-mock-name', 'some-scenario'));
});
```

### Available plugin functions
The following functions are available. Each plugin function returns a promise.

##### selectScenario(name: string, scenario: string): Promise<any>;
Selects the given scenario (when calling this function without a scenario or with 'passThrough' as scenario name, the call will be passed through to the actual backend).

##### delayResponse(mockName: string, delay: number): Promise<any>;
Sets the delay time in milliseconds for the mock. This makes sure the response is delayed. The delay set here overrides the delay defined in the response mock.

##### echoRequest(name: string, echo: boolean): Promise<any>; 
Sets the indicator which enables / disables the request logging.

##### setVariable(key: string, value: any): Promise<any>;
Adds or updates the global variable.
    
##### setVariables(variables: {[key: string]: any;}): Promise<any>;
Adds or updates the global variables  ie. {'some':'value', 'another': 'value'}.
    
##### deleteVariable(key: string): Promise<any>;
Deletes the global variable.

##### resetMocksToDefault(): Promise<any>;
Resets all the mocks to the default state.

##### setMocksToPassThrough(): Promise<any>;
Sets all the mocks to pass through.

##### setPreset(name: string): Promise<any>;
Sets the mocks and variables in the selected state.
