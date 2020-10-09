# Overview

- Start Date: 2019-12-05
- Target Major Version: 3.0
- Reference Issues: N/A
- Implementation PR: [#10313](https://github.com/vuetifyjs/vuetify/pull/10313)

## Summary

There are a number of places within the framework that make generalized calls to the window and document objects checking for their existence.

## Basic example

```js
// src/util/globals.ts

function checkForEventListenerPassiveSupport(supported = false): boolean {
  try {
    const opts = Object.defineProperty({}, 'passive', {
      get: () => (supported = true),
    })
    window.addEventListener('check', opts, opts)
    window.removeEventListener('check', opts, opts)
  } catch (e) {
    console.warn('The current browser does not support the passive option.')
    console.warn(e)
  }
  return supported
}

const IN_BROWSER = typeof window !== 'undefined'
const PASSIVE_SUPPORTED = IN_BROWSER ? checkForEventListenerPassiveSupport() : false

export {
  IN_BROWSER,
  PASSIVE_SUPPORTED,
}
```

##### UPDATE

While implementing this RFC I noticed that we check for 'IntersectionObserver' in window quite a few times. I think it would be appropriate to add it as well to the scope of this RFC.

```js
// src/utils/globals.ts

// Maybe name it INTERSECTION_OBSERVER_SUPPORTED ?
const INTERSECTION_SUPPORTED = IN_BROWSER && 'IntersectionObserver' in window

export { INTERSECTION_SUPPORTED }
```

## Motivation

DRYing up functionality that is reused throughout the framework will help with providing a clean and concise codebase.

## Detailed design

N/A

## Drawbacks

N/A

## Alternatives

N/A

## Adoption strategy

- Need to update helpers.ts to import `IN_BROWSER`

## Unresolved questions

N/A

---

All questions pertaining to this template should be directed to the Vuetify commmunity [#rfc-discussions](https://discord.gg/eXubxyJ) channel.
