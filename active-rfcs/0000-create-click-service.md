- Start Date: 2019-12-26
- Target Major Version: v3.0
- Reference Issues: N/A
- Implementation PR: (leave this empty)

## Summary

Provide a uniform way of catching global click events through the Vuetify object. 

## Basic Example

Click outside directive changes:

```tsx
const inserted = (el, binding, { $vuetify = {} }) => {
  if (!$vuetify.click) {
    consoleWarn('Unable to find the Vuetify Scroll service')

    return
  }

  el.__click = Symbol()

  $vuetify.click.register(
    el.__click,
    binding.value,
  )
}

const unbind = (el, binding, { $vuetify = {} }) => {
  if (!$vuetify.click) return

  $vuetify.click.unregister(el.__click)

  delete el.__click
}

export {
  inserted,
  unbind,
}
```

## Motivation

- Provide user with a global way of catching any global click event
- Scope `v-click-outside` directive functionality to the same process
- Creates a normalized interface for possible future features
    - e.g. **vuex-router-sync** for Vuetify

## Drawbacks

N/A

## Adoption Strategy

N/A

## Unresolved Questions

If applicable, what aspects of this proposal are still TBD?