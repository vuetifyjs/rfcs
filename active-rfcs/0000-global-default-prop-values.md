# Overview

- Start Date: 2020-10-02
- Target Major Version: 3.x
- Reference Issues: https://github.com/vuetifyjs/vuetify/issues/9677
- Implementation PR:

## Summary

This feature will allow users to define global default values for each component prop.

## Basic example

```js
const vuetify = createVuetify({
  defaults: {
    _global: {
      ripple: false,
      dense: true,
    },
    VBtn: {
      outlined: true,
    },
    VSheet: {
      elevation: 10,
    },
  },
})
```

```html
v2.x
<template>
  <v-btn outlined :ripple="false">click me</v-btn>
  <v-sheet :elevation="10">foo</v-sheet>
  <v-sheet :elevation="10">bar</v-sheet>
  <v-text-field dense />
  <v-checkbox dense />
</template>

v3.x
<template>
  <v-btn>click me</v-btn>
  <v-sheet>foo</v-sheet>
  <v-sheet>bar</v-sheet>
  <v-text-field />
  <v-checkbox />
</template>
```

## Motivation

This is a frequently requested feature, and it aligns well with the goal of making 3.x a more configurable library.

It greatly simplifies the work of having identical looking and behaving components across your project. Existing solutions are either duplicating prop values each time a specific component is used, or creating wrapper components. Both of these involve a lot of unnecessary boilerplate code.

## Detailed design

The proposed implementation uses a function `makeProps` which wraps the normal props definition object for a Vuetify component.

```js
export default defineComponent({
  props: makeProps({
    elevation: {
      type: String,
      default: 2,
    },
  })
})
```

This function will replace each prop's `default` property with a factory function. This factory function will use `inject` to fetch and return the globally set default value for that prop, if one has been defined. If a global default has not been defined, the component default will be returned instead.

Additionally, some props are so widely used across components that it might be a good idea to offer a simple way of setting a shared value for them in a single location, instead of having to define it for each individual component. See the `_global` section of the `defaults` object in the basic example. The factory function would first check here before continuing.

This implementation allows for a seamless experience when authoring Vuetify components. Component definitions look just like they do in regular Vue, with one exception. `Function` props will have to define their type as `[Function]`. Otherwise Vue will think the factory function we create in `makeProps` is just the regular default value of the prop, and it will not run on component creation.

The `makeProps` function should accept both shortform and object definitions.

```js
export default defineComponent({
  props: makeProps({
    foo: String,
    bar: {
      type: Number,
      default: 2,
    },
  })
})
```

Any composables that include functions for generating props should return the props in the standard Vue definition, so that the only calls to `makeProps` are made when defining Vuetify components. This will reduce the amount of code changes needed if we in the future need to move away from this solution.

```js
export default defineComponent({
  props: makeProps({
    foo: {
      type: String,
      default: 'bar',
    },
    ...makeElevationProps(),
  })
})
```

## Drawbacks

The implementation cost of this feature is relatively low. Everything is encapsulated in the `makeProps` function, plus the `provide` of the default values from `createVuetify`. The only modification for a component is wrapping the existing props definitions.

We should keep an eye on potential performance issues of replacing every prop default value with a factory function that will be called every time each component is created.

This should not be a breaking change. Users migrating can choose to set global default values if they want. If they do not, component defined default values will be used instead.

## Alternatives

Some earlier designs include:

- Manually calling a function for each default value
  ```js
  props: {
    foo: {
      type: String,
      default: createDefault('foo', 'component default'),
    },
  },

  props: {
    ...makeProp('foo', {
      type: String,
      default: 'component default',
    }),
  }
  ```

- Calling a function in `setup` that patches the `props` object
  ```js
  setup (props) {
    const patchedProps = patchWithGlobalDefaults(props)
  }
  ```

These were all not as ergonomic and/or more invasive than the final design.

## Adoption strategy

No adoption strategy is required for users of Vuetify

## Unresolved questions

- There might be some unresolved questions around Typescript support when it comes to typing the `defaults` property in the `createVuetify()` call. We need to be able to define and export a component's props to be reused.

- Better name than `_global`?