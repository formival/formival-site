---
layout: default
title: Usage
nav_order: 2
description: "How to get started using Formival for Vue"
permalink: /usage
---

# Usage

There are a few steps to getting going with Formival,
but it's worth it. You might not see the benefit when
designing a couple of simple forms, but once you've got
more than a few forms, you will start to see the benefits.

## Initialise

To start using Formival, the plugin is registered with
Vue using `Vue.use()` as well as an instance being
created with the options and passed to the Vue 
constructor:

```js
import Vue from 'vue';
import Formival from 'formival';

Vue.use(Formival);
const formival = new Formival({
  // options, including:
  //     types,
  //     wrappers,
  //     validationMessages
});

new Vue({
  formival,
  render: h => h(App),
}).$mount('#app');
```

This is similar to how you might initialise
Vuex or Vue Router.

Formival will not do anything without defining field types.
You will also probably want to provide at least one wrapper,
and some validation message templates. 

## Add the Formival Form Component

Then you can make use of the `formival-form` component to 
embed a form anywhere:

```html
<form @submit.prevent="onSubmit" novalidate autocomplete="off">
  <formival-form v-model="model" :validation="$v.model" :fields="fields"/>
  <button type="submit">Submit</button>
</form>
```

The `:fields` binding defines the structure of the form. 
Each field has a unique `key` that defines which bit of the 
model should be bound to this field. The `type` defines
which input component is used. And `templateOptions` defines
any extra options that are passed along to the input and wrapper
components:

```js
      fields: [
        {
          key: 'email',
          type: 'input',
          templateOptions: {
            label: 'Email',
            type: 'email'
          }
        },
        {
          key: 'password',
          type: 'input',
          templateOptions: {
            label: 'Password',
            type: 'password',
            description: 'Please enter your password here'
          }
        }
      ]
    }
  }
```

The `model` is an object who's entries will be bound to the 
form fields as defined in `fields`. The model is bound using
the `v-model` directive so that it is a two-way data binding.

```js
  data() {
    return {
      model: {
        email: 'npm@daz.is',
        password: ''
      },
    ...
  }
```

The `:validation` binding is passed a 
[Vuelidate](https://vuelidate.js.org) validation object. 
You create this by adding `validations` to the 
component options, then accessing it via `$v`.

```js
import {required, minLength, email} from "vuelidate/lib/validators";
...
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
...
```

## Configuration

Formival has no opinions about what your form markup should look
like. You need to provide your own components for the input form
controls. Formival will take care of binding them to the appropriate
parts of the model.

Define `types` for input field types. You can use `wrappers` which
are wrapped around the input fields to provide labels and 
validation error messages etc. The use of wrappers means that you can
keep it DRY and not duplicate the same elements in each of the form
controls. Validation messages use Lodash template strings and have 
access to the current `value` of the errored field, the `field`
config, and the `key` of the validator that failed.

```js
const types = [
  {
    name: 'input',
    component: SimpleInput,
    wrappers: ['field-wrapper']
  }
];

const wrappers = [
  {
    name: 'field-wrapper',
    component: FieldWrapper
  }
];

const validationMessages = {
  required: "{% raw %}{{field.templateOptions.label}}{% endraw %} is required",
  email: "{% raw %}{{value}}{% endraw %} is not a valid email address"
};

const formival = new Formival({
  types,
  wrappers,
  validationMessages
});
```

## A Simple Input

See [input types](/input-types) for more details.

```html
<template>
    <input :value="value" :id="id" :type="inputType"
           @change="$emit('touched')"
           @focus="$emit('reset')"
           @input="$emit('input', $event.target.value)">
</template>

<script>
  export default {
    name: "SimpleInput",
    props: ['value', 'field', 'id'],
    computed: {
      inputType() {
        return this.field.templateOptions.type || 'text';
      }
    }
  };
</script>
```

## A Simple Wrapper

See [wrappers](/wrappers) for more details.

```html
<template>
    <div>
        <label :for="id">{{ field.templateOptions.label }}</label>
        <slot></slot>
        <p v-if="hasError" class="error">{{ errorMessage }}</p>
    </div>
</template>

<script>
  export default {
    name: "FieldWrapper",
    props: ['field', 'id', 'hasError', 'errorMessage']
  };
</script>
```
