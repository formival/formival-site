---
layout: default
title: Conditional Fields
nav_order: 6
description: "How to get started using Formival for Vue"
permalink: /conditional-fields
---

# Conditional Fields

Use Vue's computed properties to enable conditional 
fields within your forms.

In this example, see how the `fields` that were original defined
in options are now defined as `fields()` within the computed
properties. This allows logic to be included that references
the current `this.model` form model values.

In this example, this is used to show and hide the additional
text input control:

[![Edit vue-formival-example-conditional-fields](https://codesandbox.io/static/img/play-codesandbox.svg)](https://codesandbox.io/s/vue-formival-example-conditional-fields-wm7ol?fontsize=14&hidenavigation=1&theme=dark)

<iframe src="https://codesandbox.io/embed/vue-formival-example-conditional-fields-wm7ol?fontsize=14&hidenavigation=1&theme=dark" style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;" title="vue-formival-example-conditional-fields"></iframe>

