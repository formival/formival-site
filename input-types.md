---
layout: default
title: Input Types
nav_order: 3
description: "Formival is a dynamic form library for Vue"
permalink: /input-types
---

# Input Types

Inputs are automatically bound to the correct part of the model using
the `v-model` directive. Therefore you can use any component within
your form that has been designed to work with `v-model`. Basically
`v-model` is short hand for binding on the `value` prop and emitting 
and `input` event when things change. 

In order to define your own field input type for use with Formival
you just need to accept the `value` as a prop, and `$emit` the 
new value as an `input` event when things change.

You can also take the resolved `field` config as a prop, inside
which you will find the `templateOptions` for any custom config
passed to this component, such as field labels or placeholders.

To support validation you can emit a `touched` event to signal
to Vuelidate that is should check the value and update the error
status if needed. Emitting a `reset` event will reset the error
status.

To display error information you should accept the `hasError` 
property, which will be `true` if there input is in an error
state. There is also a `errorMessage` property, but this is usually
displayed in a field wrapper.

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
