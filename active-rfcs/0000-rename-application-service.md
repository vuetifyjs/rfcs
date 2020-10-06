# Overview

- Start Date: 2019-12-23
- Target Major Version: v3.0
- Reference Issues: N/A
- Implementation PR: (leave this empty)

## Summary

Rename the application service to layout.

## Basic example

Rename the application service to layout.

```js
// v2.2
$vuetify.application.top

// v3.0
$vuetify.layout.top
```

## Motivation

The application service only deals with layouts. Should have a name more representative of what it does. There are very few use cases in which a user would want to reference the application service.

## Detailed design

N/A

## Drawbacks

- Requires the user to change all references of `$vuetify.application` to `$vuetify.layout`.

## Alternatives

What other designs have been considered? What is the impact of not doing this?

## Adoption strategy

- Change all references of `$vuetify.application` to `$vuetify.layout`.

## Unresolved questions

N/A

---

All questions pertaining to this template should be directed to the Vuetify commmunity [#rfc-discussions](https://discord.gg/eXubxyJ) channel.
