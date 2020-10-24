# Overview

- Start Date: 2020-10-25
- Target Major Version: 2.0
- Reference Issues: https://github.com/vuetifyjs/vuetify/issues/12467
- Implementation PR: (leave this empty)

## Summary

Currently the direction of components (ltr or rtl) is taken from the global Vuetify
configuration and there is no way to set an exception for a component and set its
direction separately.

This feature makes it possible to set the direction for components explicitly using
boolean props `ltr` and `rtl`.

## Basic example

For example if we had set `rtl` to `true` in the global Vuetify configuration but
we need a text field in a form to be `ltr`, we should be able to do it like this: 

```js
<v-text-field
    label="Email"
    ltr
/>
```

## Motivation

It is very helpful to be able to set the direction of Vuetify globally from a
single place in global configuration. But if the direction is set to `rtl`, in many
situations you need to be able to set the direction of some field to `ltr`.

For example you may want to have an email or URL input in your form. This fields have
to be `ltr` but you can't do this simply just by setting the `direction` property in
their style to `ltr` because the bidirectionality support in Vuetify depends on:

1. The global configuration option `rtl`
2. The global classes `v-application--is-rtl` and `v-application--is-ltr`

Which none of them can are controlled by the user. So currently there is no clean and
none-hacky way to set the direction for components separately.

## Detailed design

Similar functionality currently exists in Vuetify for theme mode (dark and light).
While we can set the theme mode in the global Vuetify configuration by setting the `theme.dark`
to `true`, but we also have the ability to set the theme mode to `dark` or `light` for each
component separately by setting their corresponding props to `true`. Exactly the same design
can be used to implement this functionality for the `direction`.

This functionality for the themes, is implemented using the Vue's provider API. Components that
have the ability to have different theme modes implement a Vue mixin called 'Themeable'. Themeable components inject a boolean value `isDark` from their ancestors and provide it to all their descendants. So each Themeable component has access
to a value `isDark` which is provided to it from its nearest ancestor or from the global Vuetify configuration.

Exactly the same thing can be implemented for the direction. Components that can have different directions (ltr or rtl)
should extend a Vue mixin which can be called `Directionable`. A Directionable component injects a boolean `isRtl` from its
ancestor Directionable provider or it will fallback to the global Vuetify configuration option `rtl`. Then this component will
provide this value to its descendants. Then each Directionable can use the provided `isRtl` value to set the component layout
based on the direction.

By this design if the direction of a component is explicitly set to `rtl` all its descendents which have not an explicit direction will have the same direction.

But just having a Vue mixin which provide a boolean `isRtl` is not enough. Most of the difference between `ltr` and `rtl` comes
from the Sass style files which are not JavaScript. Currently to have bidirectionality in the styles, two sass mixins `ltr` and `rtl` are used to define styles for different directions separately. This mixins use the `v-application--is-rtl` and `v-application--is-ltr` class names to define styles. This class names are set to the root of HTML document based on the global
configuration. But if we want to have component based direction we have to be able to set a direction class for each Directionable component separately. The same thing is implemented for the Themeable components. Each Themeable component is assigned a `theme--dark` or `theme--light` class name based on its theme mode. And then a Sass mixin called `theme` is used in the Sass files to define different styles for different theme modes.

So we should have `direction--rtl` and `direction--rtl` class names for each Directionable component which is assigned to them according to their provided direction. Then we should have a mixin called `direction` to have the ability to define a separate style for separate directions. The `direction` mixin can be used like this in the Sass files:

```Sass
+direction(v-chips) using ($direction, $start, $end)
  padding-#{$start}: 20px
  padding-#{$end}: 10px
```

All the styles which depend on the component's direction will be moved to the `direction` mixin.

So by making the components Directionable in their SFC file by extending the Directionable mixin and by modifying its corresponding Sass file so that all its direction dependant styles go into the Sass `direction` mixin we are able to give
the component the ability to have a separate direction for itself and to provide that direction to all its descendants.

## Drawbacks

Being able to set the direction globally is not enough. In many situations for Vuetify applications with `rtl` direction it is
necessary to have fields and components with `ltr` direction.

Implementing this from the user side is not possible and too hacky. for example users may try to change the direction using the
CSS styles but many bidirectional features in components depend on JavaScript and the global configuration option `ltr` and since the user has not access to the component's implementation he can't change that.

Another problem that setting the direction by style or props from the user side has is that this direction change is only applied
to the component itself and all the descendant components still will get their direction from the globel `rtl` option and from the `v-application--is-rtl` or `v-application--is-ltr` classes and the intended direction will not cascade to the subcomponents.

The implementation of this feature takes 2 steps:

1. Create the `Directionable` Vue mixin and the `direction` sass mixin similar to mixins of the Themeable components.
2. For each component which is bidirectional, extend the Directionable mixin and refactor its corresponding Sass file so that direction dependant styles are defined in the `direction` mixin.

I have done the step 1 completely and step 2 for majority of the Vuetify components in a fork of the project. It took a lot of time but it was pretty simple and straightforward and didn't add much complexity to the project source.

It does not introduce any breaking change. But after making all the components Directionable using the new implementation, there will be no need to keep the Sass `rtl` and `ltr` mixins and `v-application--is-rtl` and `v-application--is-ltr` classes anymore, since the `direction` mixin and `direction--ltr` and `direction--rtl` classes are used instead of theme. Removing the old mixins and classes may introduce breaking change so the should be kept in the project and just deprecated.

## Alternatives

An alternative is that the user implements the components that are intended to have different direction himself and use them in his project which does not seem to be a good solution and can cause inconsistency in the design and user experience.

## Adoption strategy

There is no breaking changes so if the users want to use this feature they simply can use the `ltr` and `rtl` props on components that they want to have a different direction.

This RFC will help developers who want to use Vuetify with rtl direction with much less pain and gives them the ability to use components with ltr direction in their rtl panel without having to use hacks.

## Unresolved questions

---

All questions pertaining to this template should be directed to the Vuetify commmunity [#rfc-discussions](https://discord.gg/eXubxyJ) channel.
