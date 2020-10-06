# Overview

- Start Date: 2020-01-06
- Target Major Version: 3.0
- Reference Issues: N/A
- Implementation PR: (leave this empty)

## Summary

Remove the need to use `v-container` for the application's default gutter.

## Basic example

Demonstrate the new or changed API if applicable.

```html
<!-- v2.2 -->

<v-content>
  <v-container fluid>
    ...
  </v-container>
</v-content>

<!-- v3.0 -->

<v-content>
  ...
</v-content>

<!-- v3.0 w/ removed gutter -->
<v-content no-gutters>
	...
</v-content>
```

## Motivation

Requiring the use of `v-container` for a default gutter is an unnecessary step. **no-gutters** is in line with the naming of `v-row`.

## Detailed design

N/A

## Drawbacks

N/A

## Alternatives

N/A

## Adoption strategy

- Remove `v-container` if used for gutters
- Use the **no-gutters** prop if `v-container` wasn't used for gutters

## Unresolved questions

- Should this be used in other components that use the **padless** prop as it's essentially the same thing

---

All questions pertaining to this template should be directed to the Vuetify commmunity [#rfc-discussions](https://discord.gg/eXubxyJ) channel.
