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

Formival has no opinions about how your forms should look.
Form inputs are fully customisable. **Bring your own 
input components**, and Formival will use them to build
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
