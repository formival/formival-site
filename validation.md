---
layout: default
title: Validation
nav_order: 5
description: "Formival is a dynamic form library for Vue"
permalink: /validation
---

# Validation

Validation rules are defined on the form model. 
Vue already has an awesome model-based validation library, 
called [Vuelidate](https://vuelidate.js.org/). It makes sense for us to use that,
rather than reinvent our own validation system.

You need to install and add Vuelidate as you normally would.
This is optional, as you can make forms without validation
if you really want to.

```bash
npm install vuelidate --save
```

```js
import Vue from 'vue'
import Vuelidate from 'vuelidate'
Vue.use(Vuelidate)
```

## Validation Message Configuration

You will need to configure `validationMessages` on the main
Formival instance, so that it knows how to display messages
to users when things go wrong. 

If you don't configure a validationMessage for a particular
validator, then the validator's key is used. For example,
if you add a `required` validator, but no message is configured
for `required` then the user will see the text `required` instead
of an error message.

Global error messages are defined on the main Formival instance,
by passing `validationMessages` object to the constructor:

```js
const validationMessages = {
  required: "\{{field.templateOptions.label\}} is required",
  email: "\{{value\}} is not a valid email address"
};

const formival = new Formival({
  types,
  wrappers,
  validationMessages
});

new Vue({
  formival,
  render: h => h(App),
}).$mount('#app');
```

Validation messages are defined as Lodash template strings using
the `{{` and `}}` as delimiters. The `field` configuration and
the current `value` are available to use in message templates.

## Validation Rules Configuration

The configuration of validation rules for a particular form model
is exactly the same as you would expect when using the Vuelidate
library. The validation object is added to the component options, 
passing in validators as an object that matches the expected 
structure of the form model that was defined in the data option
of the component:

```js
import {required, minLength, email} from "vuelidate/lib/validators";

  validations: {
    model: {
      email: {
        required,
        email
      },
      password: {
        required,
        minLength: minLength(8)
      }
    }
  },
```

If an input doesn't pass validation, then the key of the validator
is used to look up the validation message to display. 

## Field Customisation

Error messages can be overridden on a per-field basis by
defining `validationMessages` on the individual field config:

```js
{
  key: 'email',
  type: 'input',
  templateOptions: {
    label: 'Email',
    type: 'email'
  },
  validationMessages: {
    email: "Hey, please give us an email address!"
  }
}
```

