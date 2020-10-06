# Overview

- Start Date: 2020-01-03
- Target Major Version: 3.0
- Reference Issues: N/A
- Implementation PR: (leave this empty)

## Summary

More to follow

## Basic example

Updated theme list:

```jsx
$standard-light: (
  'bg': map-get($shades, 'black'),
  'color': map-get($shades, 'white')
);

$material: (
  'dividers': rgba(map-get($shades, 'black'), 0.12),
  'text': (
    'dark': map-get($shades, 'black'),
    'disabled': rgba(map-get($shades, 'black'), 0.38),
    'light': map-get($shades, 'white'),
    'muted': rgba(map-get($shades, 'black'), 0.6),
    'on-primary': map-get($shades, 'white'),
    'on-secondary': map-get($shades, 'black'),
    'on-bg': map-get($shades, 'black'),
    'on-surface': map-get($shades, 'black'),
    'on-error': map-get($shades, 'white')
  )
);
```

## Motivation

Why is this change necessary? What does it improve within the framework?

## Detailed design

This is the bulk of the RFC. Explain the design in enough detail for somebody
familiar with Vue to understand, and for somebody familiar with the
implementation to implement. This should get into specifics and corner-cases,
and include examples of how the feature is used. Any new terminology should be
defined here.

## Drawbacks

Why is this change necessary? What does it improve within the framework?

- implementation cost, both in term of code size and complexity
- whether the proposed feature can be implemented in userland
- integration of this feature with other existing and planned features
- cost of migrating existing Vuetify applications (is it a breaking change?)

There are tradeoffs to choosing any path. Attempt to identify them here.

## Alternatives

What other designs have been considered? What is the impact of not doing this?

## Adoption strategy

If this proposal is implemented, please consider the following:

- What steps would existing Vuetify users need to take in order to upgrade their project?
- How does this RFC affect projects in the Vuetify ecosystem?
- Can we implement a change into [eslint-plugin-vuetify](https://github.com/vuetifyjs/eslint-plugin-vuetify)

## Unresolved questions

If applicable, what aspects of this proposal are still TBD?

---

All questions pertaining to this template should be directed to the Vuetify commmunity [#rfc-discussions](https://discord.gg/eXubxyJ) channel.
