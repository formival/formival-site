---
layout: default
title: Wrappers
nav_order: 4
description: "Formival is a dynamic form library for Vue"
permalink: /wrappers
---

# Wrappers

Field wrappers allow a set of input types to share some common
markup. It is common for fields to share placement of things
like labels, help texts, and error messages.

For labels, you will accept the `field` prop, and then check 
for the custom field configuration inside `templateOptions`.
A unique `id` prop is calculated and passed to both the 
input type component and it's associated wrappers so that 
labels can be connected to the appropriate input using the `for` attribute.

Error messages are displayed by accepting the `hasError` boolean
prop and the `errorMessage` string prop.

The wrapper component must display the `<slot>` within it's 
template as this is where the inner input type will go. 

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

Wrappers are defined in the Formival config by setting the
`wrappers` array on the type definition. It is possible to 
assign multiple wrappers for a type, and they will all be applied
in order, wrapping each other and then in the middle the 
actual input type component.
