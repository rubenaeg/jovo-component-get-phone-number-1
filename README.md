# Jovo Conversational Component: GetPhoneNumber

## Getting Started

The component provides a prepackaged solution to get your user's phone number.

> [Find out more about Jovo's Conversational Components](https://www.jovo.tech/docs/components)

### Installation

You can install the component using npm:

```sh
$ npm install --save jovo-component-get-phone-number
```

After that, you use the Jovo CLI to transfer the component's files to your project using te `load` command:

```sh
$ jovo load jovo-component-get-phone-number
```

Last but not least you have to include the component in your `app.js`:

```js
// @language=typescript
// src/app.ts

import { GetPhoneNumber } from './components/jovo-component-get-phone-number';

app.useComponents(new GetPhoneNumber());

// @language=javascript
// src/app.js

const { GetPhoneNumber } = require("../components/jovo-component-get-phone-number/index");

app.useComponents(new GetPhoneNumber());
```

## Sample Dialog

SSML tags are not included in sample dialogs, but might be included in the responses.

<details>
<summary>Sample Dialog #1</summary>

User | Alexa Speech | Alexa Reprompt | Keys
--- | --- | --- | -
&nbsp; | Please tell me your phone number. | &nbsp; | start-question
It's 0123456789 | &nbsp; | &nbsp; | &nbsp;
&nbsp; | OK, I got {{phoneNumber}}. Is that correct? | Is your phone number really {{phoneNumber}} | confirm-question, confirm-reprompt
Yes. | &nbsp; | &nbsp; | &nbsp; 

</details>

<details>
<summary>Sample Dialog #2</summary>

User | Alexa Speech | Alexa Reprompt | Keys
--- | --- | --- | -
&nbsp; | Please tell me your phone number. | &nbsp; | start-question
It's 0123456789 | &nbsp; | &nbsp; | &nbsp;
&nbsp; | OK, I got {{phoneNumber}}. Is that correct? | Is your phone number really {{phoneNumber}} | confirm-question, confirm-reprompt
No | &nbsp; | &nbsp; | &nbsp; 
&nbsp; | Alright, let's try again. What is your phone number? | Please tell me your phone number digit by digit. | confirm-reject, reprompt
It's 0123456789 | &nbsp; | &nbsp;| &nbsp;
&nbsp; | OK, I got {{phoneNumber}}. Is that correct? | Is your phone number really {{phoneNumber}} | confirm-question, confirm-reprompt
Yes. | &nbsp; | &nbsp; | &nbsp; 

</details>

## Response

The component's `$response` has the following interface:

```javascript
{
    status: "SUCCESSFUL" | "REJECTED" | "ERROR",
    data: {
        phoneNumber: "string" // E164 format
    }
}
```

The `data` property will only be defined, if the component was successful!

> [Find out more about Conversational Component's responses](https://www.jovo.tech/docs/components#response)

## Configuration

The component only provides one option you can configure. It's the `numberOfFails` property, determining when the component should switch to the sequence mode, where it asks the user to input their phone number in a sequence of 3 digits, instead of the whole number at once.

Inside your project's `config.js` override the default value, which is `3`:

```js
// config.js

module.exports = {
    // ...
    components: {
        GetPhoneNumberComponent: {
            numberOfFails: 5
        }
    }
};
```


> [Find out more about Conversational Component's configuration](https://www.jovo.tech/docs/components#configuration)
