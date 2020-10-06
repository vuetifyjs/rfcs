# Overview

- Start Date: 2019-12-26
- Target Major Version: v3.0
- Reference Issues: N/A
- Implementation PR: (leave this empty)

## Summary

Make /lib exports default. Move current default to /full and /es5 to /esm.

## Basic example

If the proposal involves a new or changed API, include a basic code example.
Omit this section if it's not applicable.

```js
// v2.2
import Vuetify from 'vuetify' // full
import Vuetify from 'vuetify/lib' // esm
import { VRow } from 'vuetify/es5' // cjs

// v3.0
import Vuetify from 'vuetify' // full
import Vuetify from 'vuetify/esm' // esm
import { VRow } from 'vuetify/cjs' // cjs
```

## Motivation

Improve the path for importing Vuetify features.

## Detailed design

N/A

## Drawbacks

- Could break existing code pens for github issues
- Could be considered an unnecessary breaking change for an arguable minimal gain in clarity

## Alternatives

N/a

## Adoption strategy

Change the following imports:

- `‘vuetify/lib’` import to `‘vuetify’` for es6
- `‘vuetify’` import to `‘vuetify/full’` for full
- `‘vuetify/es5’` import to `‘vuetify/esm’`

## Unresolved questions

- Not entirely sure of all the implications of the changes for cdn usage

---

All questions pertaining to this template should be directed to the Vuetify commmunity [#rfc-discussions](https://discord.gg/eXubxyJ) channel.
