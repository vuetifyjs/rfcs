# Overview

- Start Date: 2019-12-22
- Target Major Version: 3.0
- Reference Issues: N/A
- Implementation PR: (leave this empty)

## Summary

Disable automatically filling themes with missing light/darken variants. Make it an explicit option to opt into.

## Basic example

Add a new property to the Theme service interface:

```ts
interface Theme {
  variants = false
}
```

By default this option would be false.

```js
import Vuetify from 'vuetify/lib'

// v3.0 would require the user to enable theme variants
export default new Vuetify({
  theme: { variants: true },
})
```

## Motivation

Variants on theme colors are a niche use-case and rarely used beyond manually defining a specific variant:

```js
import Vuetify from 'vuetify/lib'

export default new Vuetify({
  theme: {
    themes: {
      light: {
        primary: {
          base: 'blue',
          darken1: 'darkblue',
        },
      },
    },
  },
})
```

## Detailed design

N/A

## Drawbacks

- Users would have to opt in for the feature
- Have to create a solution for `v-slider` which uses `primary lighten-3`

## Alternatives

N/A

## Adoption strategy

- Add the **variants** option to the theme options with a value of `true`

```js
import Vuetify from 'vuetify/lib'

export default new Vuetify({
  theme: { variants: true },
  ...
})
```

## Unresolved questions

N/A

---

All questions pertaining to this template should be directed to the Vuetify commmunity [#rfc-discussions](https://discord.gg/eXubxyJ) channel.
