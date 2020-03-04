---
layout: default
title: Home
nav_order: 1
description: "Formival is a dynamic form library for Vue"
permalink: /
---

# <img src="https://formival.github.io/formival.png" alt="logo" width="100"/> Formival


As web app developers, we spend a lot of our time
building forms. What if building forms could be 
productive and fun? 


[![npm](https://badgen.net/npm/v/formival)](https://www.npmjs.com/package/formival) 
[![size](https://badgen.net/bundlephobia/minzip/formival)](https://bundlephobia.com/result?p=formival)
[![tests](https://badgen.net/travis/formival/formival)](https://travis-ci.org/formival/formival)
[![coverage](https://badgen.net/codecov/c/gh/formival/formival)](https://codecov.io/gh/formival/formival)
[![analysis](https://img.shields.io/scrutinizer/quality/g/formival/formival?style=flat-square)](https://scrutinizer-ci.com/g/formival/formival/)
[![Codacy Badge](https://api.codacy.com/project/badge/Grade/00481f2073ed4f77a1653bd397201b49)](https://app.codacy.com/gh/formival/formival)
[![vue2](https://badgen.net/badge/Vue/2.x/green)](https://vuejs.org/)
[![license](https://badgen.net/badge/license/MIT/blue)](http://opensource.org/licenses/MIT)

## About

Formival is a dynamic forms library for Vue that 
provides automatic form generation. 
It is inspired by Formly, but reinvented as idiomatic Vue. 
We make use of the awesome Vuelidate library, rather than re-inventing a new validation solution.

You provide a config object that defines your form, and 
Formival will take care of the rest!

Form inputs are fully customisable. Bring your own 
input components, and Formival will use them to build
the form, binding them to the appropriate parts
of the form model. Provide validations for the form
model and the appropriate validation results will
be passed to the appropriate parts of the form.

## Installation

For use with Vue CLI projects, Webpack, or Rollup,
install the package from npm:

```bash
npm install --save formival
```

Or, you can use directly in the browser by linking 
to a CDN build:

```html
<script src="https://unpkg.com/formival"></script>
```

## Usage

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

Then you can make use of the `formival-form` component to 
embed a form anywhere:

```html
<form @submit.prevent="onSubmit" novalidate autocomplete="off">
  <formival-form v-model="model" :validation="$v.model" :fields="fields"/>
  <button type="submit">Submit</button>
</form>
```

The `:fields` binding defines the structure of the form:

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
